---
title: Winform：Graphic进行绘制
abbrlink: 101d1beb
date: 2024-02-05 00:00:00
categories:
  - [经验分享]
  - [桌面开发]
tags:
  - [Winform]
  - [教程]
  - [精选]
cover: https://p.wzsco.top/dd08624b0f13e720db403518bd46d03b.png/cover
---

## 前言

使用Winform进行窗体开发，知道WInform是基于GDI的实现。

---

## 什么是自定义控件？

在MSND上，微软对Winform的定义：Forms是Winforms应用程序的基本单元，它实质上是一块空白的面板，开发人员通过使用控件去创建用户界面，并编写代码去操作数据。.Net中对WinfowsForm编程的称谓即为Winform。



## 使用步骤

1. 创建一个类，继承Control
    ```csharp
        public class MyControl : Control{
            public MyControl(){
            }
        }
    ```
2. 重写OnPaint方法
    ```csharp
        protected override void OnPaint(PaintEventArgs e){
            // 调用父类方法。从传入的参数中获取Graphic（画板）。
            base.OnPaint(e);
            Graphics g = e.Graphics;
        }
    ```
3. 使用画笔进行绘制线段
    - 绘制线段
    ```csharp
        protected override void OnPaint(PaintEventArgs e){
                base.OnPaint(e);
                Graphics g = e.Graphics;
                // 获取当前控件的宽高
                int w = Width,h = Height;
    
                // 使用using语法，因为Pen是系统占用。微软推荐使用using语法。。
                using(Pen pen = new Pen(Color.Red)){
                // 画两条对角的线
                g.DrawLine(pen, 0, 0, w, h);
                g.DrawLine(pen, w, 0, 0, h);
            }
        }
    ```
    有多种实现，具体看文档：[Graphics.DrawLine Method](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.graphics.drawline?view=dotnet-plat-ext-6.0)
    效果：![线段绘制](https://p.wzsco.top/536e87be2fc34cf88037b071364eb139.png/blogimg)
    - 绘制矩形
    ```csharp
    protected override void OnPaint(PaintEventArgs e){
        base.OnPaint(e);
        Graphics g = e.Graphics;
        int w = Width,h = Height;
            
        using(Pen pen = new Pen(Color.Red)){
            // 画长方形
            g.DrawRectangle(pen,10,10,80,30);
        }
    }
    ```
    有多种实现，具体看文档：[Graphics.DrawRectangle Method](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.graphics.drawrectangle?view=dotnet-plat-ext-6.0)
    效果：![矩形绘制](https://p.wzsco.top/a94be700abc18a24384863fdda9fae65.png/blogimg)
    - 绘制圆形（包含矩形）
    ```csharp
      protected override void OnPaint(PaintEventArgs e){
          base.OnPaint(e);
          Graphics g = e.Graphics;
          int w = Width,h = Height;
            
          using (Pen pen = new Pen(Color.Orange, 2.0f)){
          g.DrawEllipse(pen, 10, 10, 30, 30);
          }
      }
    ```
    有多种实现，具体看文档：[Graphics.DrawEllipase Method](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.graphics.drawellipse?view=dotnet-plat-ext-6.0)
    效果：![绘制圆形](https://p.wzsco.top/887e55d7261ed27ffa52dbb6b0464f06.png/blogimg)

## 使用 Brush 进行填充

- 填充矩形
    ```csharp
    protected override void OnPaint(PaintEventArgs e){
        base.OnPaint(e);
        Graphics g = e.Graphics;
        int w = Width,h = Height;
        
        using (Brush brush = new SolidBrush(Color.LightSkyBlue)){
          g.FillRectangle(brush, 10,10,80.30);
        }
    }
    ```
    有多种实现，具体看文档：[Graphics.FillRectangle Method](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.graphics.fillrectangle?view=dotnet-plat-ext-6.0)
    效果：![矩形填充](https://p.wzsco.top/c94faeda053370bb71455fa23f003b25.png/blogimg)
- 填充圆形（包含椭圆）
    ```csharp
    protected override void OnPaint(PaintEventArgs e){
        base.OnPaint(e);
        Graphics g = e.Graphics;
        int w = Width,h = Height;
        
        using (Brush brush = new SolidBrush(Color.Pink))
        {
            // 根据大小调节，绘制正圆、椭圆
            g.FillEllipse(brush, 10, 10, 80, 30);
        }
    }
    ```
    效果：![绘制圆形](https://p.wzsco.top/1cb87f6a57d3fb959ddd89f019f7d29f.png/blogimg)
    
{% note info modern no-icon %}
如果需要让绘制的图形抗锯齿，需要自己指定。
```csharp
protected override void OnPaint(PaintEventArgs e){
    base.OnPaint(e);
    Graphics g = e.Graphics;
    int w = Width,h = Height;
        
    // 平滑绘制，反锯齿
    g.SmoothingMode = SmoothingMode.HighQuality;
}
```
{% endnote %}

## 总结

使用画板是需要注意，调用的工具类都会占用系统内存，官方建议使用using()语法。

Api的格式很简洁，`Graphics.Fill` fill结尾就是填充方法。`Graphics.Draw` draw结尾就是绘制方法。