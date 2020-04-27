---
title: Cambiar iconos de indicador y conjuntos de indicadores (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8a056adf-4473-473d-9b0c-314675af7bfd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 37f3b93019a837ac5521c52e9ceb5f58f3e39b5d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106373"
---
# <a name="change-indicator-icons-and-indicator-sets-report-builder-and-ssrs"></a>Cambiar iconos de indicador y conjuntos de indicadores (Generador de informes y SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]proporciona conjuntos de indicadores preconfigurados, que es posible que no siempre representen los datos de manera eficaz y funcionen bien en el informe entregado. En este tema se ofrecen procedimientos para cambiar la apariencia de los iconos de indicador y cambiar los conjuntos de indicadores para que contengan más o menos iconos, o iconos distintos.  
  
 Opciones como los colores se pueden establecer mediante expresiones. Para más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-color-of-an-indicator-icon"></a>Para cambiar el color de un icono de indicador  
  
1.  Haga clic con el botón derecho en el indicador que quiera cambiar y seleccione **Propiedades de indicador**.  
  
2.  Haga clic en **Valores y estados** en el panel izquierdo.  
  
3.  Haga clic en la flecha hacia abajo de la columna **Color** , al lado del icono que desea cambiar, y haga clic en el color que se debe usar, en **Ningún color**o en **Más colores**.  
  
     Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece el valor de la opción **Color** .  
  
     Si hace clic en **Más colores**, se abre el cuadro de diálogo **Seleccionar color** , en el que puede elegir entre muchos colores. Para obtener más información sobre las opciones, vea [Cuadro de diálogo Seleccionar color &#40;Generador de informes y SSRS&#41;](../select-color-dialog-box-report-builder-and-ssrs.md). Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Seleccionar color** .  
  
4.  Haga clic en **OK**.  
  
### <a name="to-change-the-icon"></a>Para cambiar el icono  
  
1.  Haga clic con el botón derecho en el indicador que quiera cambiar y seleccione **Propiedades de indicador**.  
  
2.  Haga clic en **Valores y estados** en el panel izquierdo.  
  
3.  Haga clic en la flecha hacia abajo que hay al lado del icono que desea cambiar y seleccione otro icono.  
  
     Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece el valor de la opción **Icono** .  
  
4.  Haga clic en **OK**.  
  
### <a name="to-use-a-custom-image-as-an-indicator-icon"></a>Para usar una imagen personalizada como icono de indicador  
  
1.  Haga clic con el botón derecho en el indicador que quiera cambiar y seleccione **Propiedades de indicador**.  
  
2.  Haga clic en **Valores y estados** en el panel izquierdo.  
  
3.  Haga clic en la flecha hacia abajo que hay al lado del icono que desea cambiar y seleccione **Imagen**.  
  
4.  En la lista **Seleccionar el origen de la imagen** , haga clic en **Externo**, **Incrustado**o **Base de datos**.  
  
5.  Dependiendo del origen de la imagen, realice uno de los procedimientos siguientes:  
  
    -   Para utilizar una imagen almacenada fuera del informe, haga clic en **Examinar** y busque la imagen. El informe incluirá una referencia a la imagen.  
  
    -   Para utilizar una imagen que esté incrustada en el informe, haga clic en **Importar** y busque la imagen. La imagen se agregará a la definición de informe y se guardará con él.  
  
    -   Para usar una imagen que está en una base de datos, en la lista **Usar este campo** , seleccione el campo en la lista y, a continuación, en la lista **Usar este tipo MIME** , seleccione el tipo MIME de la imagen.  
  
6.  Haga clic en **OK**.  
  
### <a name="to-add-an-icon-to-the-indicator-set"></a>Para agregar un icono al conjunto de indicadores  
  
1.  Haga clic con el botón derecho en el indicador que quiera cambiar y seleccione **Propiedades de indicador**.  
  
2.  Haga clic en **Valores y estados** en el panel izquierdo.  
  
3.  Haga clic en **Agregar**. Se agrega un indicador, utilizando el icono predeterminado y la opción **Ningún color** .  
  
     Configure el indicador de forma que use el icono y el color que desee. En procedimientos anteriores de este tema se describe cómo hacerlo.  
  
4.  Haga clic en **OK**.  
  
### <a name="to-delete-an-icon-to-the-indicator-set"></a>Para eliminar un icono del conjunto de indicadores  
  
1.  Haga clic con el botón derecho en el indicador que quiera cambiar y seleccione **Propiedades de indicador**.  
  
2.  Haga clic en **Valores y estados** en el panel izquierdo.  
  
3.  Seleccione el icono que desea eliminar y haga clic en **Eliminar**.  
  
4.  Haga clic en **OK**.  
  
## <a name="see-also"></a>Consulte también  
 [Indicadores &#40;Generador de informes y SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  
