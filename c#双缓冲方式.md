# 窗口编程闪烁问题
因为绘制是擦除、绘制一系列步骤才能完成，如果擦除和绘制不在同一个时间段，就会闪烁。
## 默认缓冲
1. 使用netframework提供的默认双缓冲，需要开启。
    ```c#
    DoubleBuffered = true;
    ```
2. 或者调用Style方法将OptimizedDoubleBuffered设置为True
    ```c#
    // Set the value of the double-buffering style bits to true.
    this.SetStyle(ControlStyles.DoubleBuffer | 
        ControlStyles.UserPaint | 
        ControlStyles.AllPaintingInWmPaint,
        true);
    this.UpdateStyles();
    ```
## 手动管理缓冲
- 通过BufferedGraphicsContext来实现自己的双缓冲逻辑，每个应用程序域多数只有一个BufferGraphicsContext实例，而
这个实例被BufferedGraphicsManager管理，通过Current属性来调用默认的实例。

    1. 创建BufferedGraphicsContext实例
    ```c#
    BufferedGraphicsContext myContext;
    myContext = new BufferedGraphicsContext();
    // Insert code to create graphics here.
    // On a non-default BufferedGraphicsContext instance, you should always
    // call Dispose when finished.
    myContext.Dispose();
    ```
    2. 调用Allocate方法，创建BufferedGraphics
    ```c#
    // This example assumes the existence of a form called Form1.
    BufferedGraphicsContext currentContext;
    BufferedGraphics myBuffer;
    // Gets a reference to the current BufferedGraphicsContext
    currentContext = BufferedGraphicsManager.Current;
    // Creates a BufferedGraphics instance associated with Form1, and with
    // dimensions the same size as the drawing surface of Form1.
    myBuffer = currentContext.Allocate(this.CreateGraphics(),
    this.DisplayRectangle);
    ```
    3. 绘制图像到缓冲区中
    ```c#
    // Draws an ellipse to the graphics buffer.
    myBuffer.Graphics.DrawEllipse(Pens.Blue, this.DisplayRectangle);
    ```
    4. 调用Render显示到图面
    ```c#
    // This example assumes the existence of a BufferedGraphics instance
    // called myBuffer.
    // Renders the contents of the buffer to the drawing surface associated
    // with the buffer.
    myBuffer.Render();
    // Renders the contents of the buffer to the specified drawing surface.
    myBuffer.Render(this.CreateGraphics());
    ```

- 通过创建Bitmap，将图形绘制在bitmap上
    ```c#
    var bmp = new Bitmap(width, heigth);
    var gfx = Graphics.FromImage(bmp);


    // Drawing somethings. eg.
    gfx.DrawClear(Color.White);
    ...

    // Render
    e.graphics.DrawImage(bmp, x, y);

    // Free
    gfx.Disposed();
    bmp.Disposed();
    ```


