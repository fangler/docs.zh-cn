---
title: "Brush 变换概述"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], transformation properties
- properties [WPF], transformation
- transformation properties of brushes [WPF]
ms.assetid: 8b9bfc09-12fd-4cd5-b445-99949f27bc39
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: aa4a533594c1e89942406e7df0a49215e3885418
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="brush-transformation-overview"></a>Brush 变换概述
此画笔类提供两个转换属性：<xref:System.Windows.Media.Brush.Transform%2A>和<xref:System.Windows.Media.Brush.RelativeTransform%2A>。 使用这些属性，可以旋转、缩放、倾斜和转换画笔的内容。 本主题介绍这两个属性之间的区别，并提供有关它们的用法示例。  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>系统必备  
 若要了解本主题，应了解要转换的画笔的功能。 有关<xref:System.Windows.Media.LinearGradientBrush>和<xref:System.Windows.Media.RadialGradientBrush>，请参阅[使用纯色和渐变概述绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)。 有关<xref:System.Windows.Media.ImageBrush>， <xref:System.Windows.Media.DrawingBrush>，或<xref:System.Windows.Media.VisualBrush>，请参阅[使用图像、 图形和视觉对象进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)。 还应当熟悉[转换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)中所述的 2D 转换。  
  
<a name="transformversusrelativetransform"></a>   
## <a name="differences-between-the-transform-and-relativetransform-properties"></a>Transform 和 RelativeTransform 属性之间的区别  
 在将转换应用到画笔的<xref:System.Windows.Media.Brush.Transform%2A>属性，你需要知道所绘制区域的大小，如果你想要转换的画笔内容围绕其中心。 假设已绘制区域的宽度为 200 个与设备无关的像素，高度为 150。  如果你使用<xref:System.Windows.Media.RotateTransform>旋转画笔的输出围绕其中心的 45 度，您将为<xref:System.Windows.Media.RotateTransform><xref:System.Windows.Media.RotateTransform.CenterX%2A>的 100 和<xref:System.Windows.Media.RotateTransform.CenterY%2A>75。  
  
 在将转换应用到画笔的<xref:System.Windows.Media.Brush.RelativeTransform%2A>属性，该转换应用到画笔之前其输出映射到绘制区域。 以下列表介绍处理和转换画笔内容的顺序。  
  
1.  处理画笔的内容。 有关<xref:System.Windows.Media.GradientBrush>，这意味着确定渐变的区域。 有关<xref:System.Windows.Media.TileBrush>、<xref:System.Windows.Media.TileBrush.Viewbox%2A>映射到<xref:System.Windows.Media.TileBrush.Viewport%2A>。 这成为画笔的输出。  
  
2.  将画笔的输出投影到 1 x 1 的转换矩形上。  
  
3.  应用的画笔<xref:System.Windows.Media.Brush.RelativeTransform%2A>，如果有的话。  
  
4.  将转换后的输出投影到要绘制的区域上。  
  
5.  应用的画笔<xref:System.Windows.Media.Transform>，如果有的话。  
  
 因为<xref:System.Windows.Media.Brush.RelativeTransform%2A>施加而画笔输出映射到 1x1 矩形，转换中心和偏移量的值看起来是相对路径。 例如，如果你使用<xref:System.Windows.Media.RotateTransform>旋转画笔的输出围绕其中心的 45 度，您将为<xref:System.Windows.Media.RotateTransform> <xref:System.Windows.Media.RotateTransform.CenterX%2A> 0.5 的和<xref:System.Windows.Media.RotateTransform.CenterY%2A>为 0.5。  
  
 下图显示的旋转 45 度使用的几个画笔输出<xref:System.Windows.Media.Brush.RelativeTransform%2A>和<xref:System.Windows.Media.Brush.Transform%2A>属性。  
  
 ![RelativeTransform 和 Transform 属性](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brushrelativetransform-transform-small.png "graphicsmm_brushrelativetransform_transform_small")  
  
<a name="relativetransformandtilebrush"></a>   
## <a name="using-relativetransform-with-a-tilebrush"></a>将 RelativeTransform 用于 TileBrush  
 由于比其他画笔更复杂的平铺画笔，应用<xref:System.Windows.Media.Brush.RelativeTransform%2A>到其中一个可能会产生意外的结果。 例如以下图像。  
  
 ![源图像](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-1-original-image.jpg "graphicsmm_reltransform_1_original_image")  
  
 下面的示例使用<xref:System.Windows.Media.ImageBrush>来绘制包含前面的图像的矩形区域。 它将应用<xref:System.Windows.Media.RotateTransform>到<xref:System.Windows.Media.ImageBrush>对象的<xref:System.Windows.Media.Brush.RelativeTransform%2A>属性，并设置其<xref:System.Windows.Media.TileBrush.Stretch%2A>属性<xref:System.Windows.Media.Stretch.UniformToFill>，这应保留图像的纵横比，当它拉伸以完全填充的矩形。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMRelativeTransformExample2Inline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/RelativeTransformIllustration.xaml#graphicsmmrelativetransformexample2inline)]  
  
 该示例产生下面的输出：  
  
 ![转换后的输出](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-6-output.png "graphicsmm_reltransform_6_output")  
  
 请注意扭曲图像，即使画笔的<xref:System.Windows.Media.TileBrush.Stretch%2A>已设置为<xref:System.Windows.Media.Stretch.UniformToFill>。 这是因为后的画笔应用相对转换<xref:System.Windows.Media.TileBrush.Viewbox%2A>映射到其<xref:System.Windows.Media.TileBrush.Viewport%2A>。 以下列表介绍该过程的每个步骤：  
  
1.  项目画笔的内容 (<xref:System.Windows.Media.TileBrush.Viewbox%2A>) 到其基本磁贴 (<xref:System.Windows.Media.TileBrush.Viewport%2A>) 使用画笔的<xref:System.Windows.Media.TileBrush.Stretch%2A>设置。  
  
     ![拉伸 Viewbox 以适合于视区](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-2-viewbox-to-viewport.png "graphicsmm_reltransform_2_viewbox_to_viewport")  
  
2.  将基本图块投影到 1 x 1 的转换矩形上。  
  
     ![将 Viewport 映射到转换矩形](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-3-output-to-transform.png "graphicsmm_reltransform_3_output_to_transform")  
  
3.  应用<xref:System.Windows.Media.RotateTransform>。  
  
     ![应用相对转换 ](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-4-transform-rotate.png "graphicsmm_reltransform_4_transform_rotate")  
  
4.  将转换后的基本图块投影到要绘制的区域上。  
  
     ![将转换后的画笔投影到输出区域上](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-5-transform-to-output.png "graphicsmm_reltransform_5_transform_to_output")  
  
<a name="rotateexample"></a>   
## <a name="example-rotate-an-imagebrush-45-degrees"></a>示例：将 ImageBrush 旋转 45 度  
 下面的示例应用<xref:System.Windows.Media.RotateTransform>到<xref:System.Windows.Media.Brush.RelativeTransform%2A>属性<xref:System.Windows.Media.ImageBrush>。 <xref:System.Windows.Media.RotateTransform>对象的<xref:System.Windows.Media.RotateTransform.CenterX%2A>和<xref:System.Windows.Media.RotateTransform.CenterY%2A>属性都设置为 0.5，此内容的中心相对坐标点。 因此，画笔的内容围绕其中心旋转。  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushrelativetransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushrelativetransformexample)]
 [!code-xaml[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushrelativetransformexample)]  
  
 下一个示例也适用<xref:System.Windows.Media.RotateTransform>到<xref:System.Windows.Media.ImageBrush>，但使用<xref:System.Windows.Media.Brush.Transform%2A>属性而不是<xref:System.Windows.Media.Brush.RelativeTransform%2A>属性。 要旋转的中心，而有关画笔<xref:System.Windows.Media.RotateTransform>对象的<xref:System.Windows.Media.RotateTransform.CenterX%2A>和<xref:System.Windows.Media.RotateTransform.CenterY%2A>必须设置为绝对坐标。 由于画笔要绘制的矩形为 175 x 90 像素，因此它的中心点为 (87.5, 45)。  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushTransformExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushtransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushTransformExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushtransformexample)]
 [!code-xaml[BrushesIntroduction_snip#ImageBrushTransformExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushtransformexample)]  
  
 下图显示而无需具有应用于转换的转换画笔<xref:System.Windows.Media.Brush.RelativeTransform%2A>属性，并应用于转换<xref:System.Windows.Media.Brush.Transform%2A>属性。  
  
 ![画笔 RelativeTransform 和 Transform 设置](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-transformandrelativetransform.png "wcpsdk_graphicsmm_transformandrelativetransform")  
  
 此示例摘自一个更大的示例。 有关完整示例，请参阅[画笔示例](http://go.microsoft.com/fwlink/?LinkID=159973)。 有关画笔的详细信息，请参阅 [WPF 画笔概述](../../../../docs/framework/wpf/graphics-multimedia/wpf-brushes-overview.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Windows.Media.Brush.Transform%2A>  
 <xref:System.Windows.Media.Brush.RelativeTransform%2A>  
 <xref:System.Windows.Media.Transform>  
 <xref:System.Windows.Media.Brush>  
 [使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)  
 [使用图像、绘图和视觉对象进行绘制](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)  
 [转换概述](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)
