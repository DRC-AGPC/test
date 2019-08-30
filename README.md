### 要使用PIE來強化影像，需要在C#中載入PIE_CLR.dll並呼叫下列函數即可

```C#
byte* PIEclr.PIEclr_enhance_image(byte* gray_image, int width, int height)
```

#### 輸入

__gray_image__: a byte pointer that points to the image with shape width*height

__width__: the width of the image

__height__: the height of the image


#### 輸出
a byte pointer that points to the image with shape 4 * width* 4 * height

#### 範例
以下是使用範例
```C#
PIEclr pie = new PIEclr();
Bitmap bmp = new Bitmap("input.bmp");

//transform bitmap to byte*
Rectangle rect = new Rectangle(0, 0, bmp.Width, bmp.Height);
System.Drawing.Imaging.BitmapData bmpData = bmp.LockBits(rect, System.Drawing.Imaging.ImageLockMode.ReadWrite, bmp.PixelFormat);
byte* p = (byte*)(void*)bmpData.Scan0;

// PIE enhancement
byte* img = pie.PIEclr_enhance_image(p, bmp.Height, bmp.Width);
```

以下解釋程式流程，首先產生一個PIEclr的物件，並讀取圖片
```
PIEclr pie = new PIEclr();
Bitmap bmp = new Bitmap("input.bmp");
```

讀取圖片為bitmap格式，將其轉為 byte*
```
//transform bitmap to byte*
Rectangle rect = new Rectangle(0, 0, bmp.Width, bmp.Height);
System.Drawing.Imaging.BitmapData bmpData = bmp.LockBits(rect, System.Drawing.Imaging.ImageLockMode.ReadWrite, bmp.PixelFormat);
byte* p = (byte*)(void*)bmpData.Scan0;
```

最後運用PIE將圖片提升解析度
```
// PIE enhancement
byte* img = pie.PIEclr_enhance_image(p, bmp.Height, bmp.Width);
```
