---
title: 'HelloData: una aplicación ADO simple | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 18f9f0cd227a258b1d2d9cd2d201527f614bcc49
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758831"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: una aplicación ADO sencilla
Esta sencilla aplicación se guía a través de cada una de las cuatro operaciones de ADO principales: obtener, examinar, editar y actualizar datos. Estas operaciones se realizan en la base de datos de ejemplo Northwind incluida en Microsoft® SQL Server. Para centrarse en los aspectos básicos de ADO y evitar la confusión del código, el control de errores en el ejemplo es mínimo.  
  
### <a name="to-run-hellodata"></a>Para ejecutar HelloData  
  
1.  Cree un nuevo EXE estándar Visual Basic proyecto que haga referencia a la biblioteca de ADO. Para obtener más información, vea [hacer referencia a las bibliotecas de ADO](../../../ado/guide/referencing-the-ado-libraries.md).  
  
2.  Cree cuatro botones de comando en la parte superior del formulario, estableciendo las propiedades **Name** y **Caption** en los valores que se muestran en la tabla al final de este tema.  
  
3.  Debajo de los botones, agregue un **control DataGrid de Microsoft** (Msdatgrd. ocx). El archivo Msdatgrd. ocx se incluye con Visual Basic y se encuentra en el directorio \windows\system32. o \Winnt\System32. Para agregar el control DataGrid al panel cuadro de herramientas de Visual Basic, seleccione **componentes...** en el menú **proyecto** . Después, active la casilla situada junto a "control DataGrid de Microsoft 6,0 (SP3) (OLEDB)" y, a continuación, haga clic en **Aceptar**. Para agregar el control al proyecto, arrastre el control DataGrid desde el cuadro de herramientas al formulario Visual Basic.  
  
4.  Cree un **cuadro de texto** en el formulario debajo de la cuadrícula y establezca sus propiedades como se muestra en la tabla. Cuando haya terminado, el formulario debería ser similar a la siguiente ilustración.  
  
5.  Por último, copie el código que aparece en el [código HelloData](../../../ado/guide/data/hellodata-code.md)y péguelo en la ventana Editor de código del formulario. Presione **F5** para ejecutar el código.  
  
> [!NOTE]
>  En el ejemplo siguiente, y a lo largo de la guía, se usa el ID. de usuario "MyId" con la contraseña "123aBc" para autenticarse en el servidor. Debe sustituir estos valores por credenciales de inicio de sesión válidas para el servidor. Además, sustituya el valor de "mi SQLServer" por el nombre del servidor.  
  
 Para obtener una descripción detallada del código, vea [comentarios sobre HelloData](../../../ado/guide/data/comments-on-hellodata.md).  
  
 ![Muestra Form1 para la aplicación HelloData de VB](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|Tipo de control|Propiedad|Valor|  
|------------------|--------------|-----------|  
|Form|Name|Form1|  
||Alto|6500|  
||Ancho|6500|  
|DataGrid de MS|Name|grdDisplay1|  
|TextBox|Name|txtDisplay1|  
||Multiline|true|  
|Botón de comando|Name|cmdGetData|  
||Caption|Get Data|  
|Botón de comando|Name|cmdExamineData|  
||Caption|Examinar datos|  
|Botón de comando|Name|cmdEditData|  
||Caption| Editar datos|  
|Botón de comando|Name|cmdUpdateData|  
||Caption|Datos actualizados|
