---
updated: '2025-01-07T13:46:00.000Z'
date: '2024-10-23T15:34:00.000Z'
categories: Android
urlname: android_textview_under_line
tags:
  - Android
title: TextView自定义下划线
cover: 'https://cn.bing.com/th?id=OHR.ElephantTeacher_EN-US8363933732_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

# 方案一：使用`LineBackgroundSpan`


```kotlin
/**
 * 自定义下划线背景 Span，用于绘制具有自定义颜色、厚度和偏移量的下划线。
 * 支持跨多行文本的下划线绘制。
 */
class CustomUnderlineByLineBackgroundSpan(
    private val underlineColor: Int = Color.BLACK,
    private val underlineThickness: Float = 5f,
    private val underlineOffset: Float = 0f
) : LineBackgroundSpan {

    override fun drawBackground(
        canvas: Canvas,
        paint: Paint,
        left: Int,       // 文本区域的左边界
        right: Int,      // 文本区域的右边界
        top: Int,        // 文本区域的顶部
        baseline: Int,   // 基线
        bottom: Int,     // 文本区域的底部
        text: CharSequence,
        lineStart: Int,  // 当前行在文本中的起始索引
        lineEnd: Int,    // 当前行在文本中的结束索引
        lineNumber: Int
    ) {
        // 确保文本是 Spanned 类型
        if (text !is Spanned) return

        // 获取当前 Span 在整个文本中的起始和结束位置
        val spanStart = text.getSpanStart(this)
        val spanEnd = text.getSpanEnd(this)

        // 计算当前行与 Span 的重叠范围
        val drawStart = maxOf(lineStart, spanStart)
        val drawEnd = minOf(lineEnd, spanEnd)

        // 如果当前行没有覆盖 Span 的任何部分，则无需绘制下划线
        if (drawStart >= drawEnd) {
            return
        }

        // 计算相对于当前行的绘制起始和结束位置
        val relativeStart = drawStart - lineStart
        val relativeEnd = drawEnd - lineStart

        // 保存原始 Paint 的颜色和线宽
        val originalColor = paint.color
        val originalStrokeWidth = paint.strokeWidth

        try {
            // 设置下划线的颜色和厚度
            paint.color = underlineColor
            paint.strokeWidth = underlineThickness

            // 计算下划线的 Y 坐标
            val underlineY = baseline + paint.fontMetrics.descent - underlineThickness / 2 + underlineOffset

            // 使用 Paint 的 measureText 直接测量从行起始到 drawStart 和 drawEnd 的宽度
            val xStart = left + paint.measureText(text, lineStart, drawStart)
            val xEnd = left + paint.measureText(text, lineStart, drawEnd)

            // 绘制下划线
            canvas.drawLine(xStart, underlineY, xEnd, underlineY, paint)
        } finally {
            // 确保 Paint 的原始颜色和线宽被恢复
            paint.color = originalColor
            paint.strokeWidth = originalStrokeWidth
        }
    }
}
```


这个方案在某些设备上会出现下划线比文字短的情况，所以只能继续想其他方案了


# 方案二：使用`ReplacementSpan`


```kotlin
/**
 * 可自定义下划线属性的 Span
 * 缺点：无法实现跨行下划线，如果要实现跨行下划线，请对每一个行内的字符设置 CustomUnderlineSpan
 *
 * @property underlineColor 下划线的颜色
 * @property underlineThickness 下划线的厚度
 * @property underlineOffset 偏移量，大于 0 时向下偏移，小于 0 时向上偏移
 */
class CustomUnderlineByReplacementSpan(
    private val textColor: Int = Color.BLACK,
    private val underlineColor: Int = Color.BLACK,
    private val underlineThickness: Float = 5f,
    private val underlineOffset: Float = 0f,
) : ReplacementSpan() {
    override fun getSize(
        paint: Paint,
        text: CharSequence,
        start: Int,
        end: Int,
        fm: Paint.FontMetricsInt?,
    ): Int = (paint.measureText(text, start, end)).toInt()

    override fun draw(
        canvas: Canvas,
        text: CharSequence,
        start: Int,
        end: Int,
        x: Float,
        top: Int,
        y: Int,
        bottom: Int,
        paint: Paint,
    ) {
        // 设置下划线的颜色和厚度
        paint.color = underlineColor
        paint.strokeWidth = underlineThickness

        // 计算下划线的 Y 坐标
        val underlineY = y + paint.fontMetrics.descent - underlineThickness / 2 + underlineOffset

        // 绘制下划线
        canvas.drawLine(x, underlineY, x + paint.measureText(text, start, end), underlineY, paint)

        // 因为ReplacementSpan的优先级比较高，会覆盖之前使用的ForegroundColorSpan，所以这里需要重新设置一下颜色
        paint.color = textColor

        // 绘制文本
        canvas.drawText(text, start, end, x, y.toFloat(), paint)
    }
}
```


`ReplacementSpan` 由于没办法换行，所以使用的时候，如果是多行文本，需要对每一个字符设置Span

