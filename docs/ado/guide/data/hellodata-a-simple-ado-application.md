---
title: 'HelloData: Una aplicación ADO Simple | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 97957adf53cfea64693530b79920dd54d6d0a1bf
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700638"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: una aplicación ADO sencilla
Los pasos de esta aplicación simple a través de cada una de las cuatro operaciones principales de ADO: introducción, examinar, editar y actualizar datos. Estas operaciones se realizan en la base de datos de ejemplo Northwind incluido con Microsoft® SQL Server. Para centrarse en los aspectos básicos de ADO y evitar el desorden de código, control de errores en el ejemplo es mínimo.  
  
### <a name="to-run-hellodata"></a>Para ejecutar HelloData  
  
1.  Cree un nuevo proyecto de Visual Basic de EXE estándar que hace referencia a la biblioteca ADO. Para obtener más información, consulte [que hacen referencia a las bibliotecas de ADO](../../../ado/guide/referencing-the-ado-libraries.md).  
  
2.  Cree cuatro botones de comando en la parte superior del formulario, estableciendo el **nombre** y **título** propiedades según los valores mostrados en la tabla al final de este tema.  
  
3.  Debajo de los botones, agregue un **Microsoft DataGrid Control** (Msdatgrd.ocx). El archivo Msdatgrd.ocx se incluye con Visual Basic y se encuentra en el directorio \windows\system32 o \winnt\system32. Para agregar el control DataGrid a su panel de cuadro de herramientas de Visual Basic, seleccione **componentes...**  desde el **proyecto** menú. A continuación, active la casilla junto a "Microsoft DataGrid Control 6.0 (SP3) (OLEDB)" y, a continuación, haga clic en **Aceptar**. Para agregar el control al proyecto, arrastre el control DataGrid de formularios en el cuadro de herramientas hasta el formulario de Visual Basic.  
  
4.  Crear un **TextBox** en el formulario debajo de la cuadrícula y establezca sus propiedades como se muestra en la tabla. El formato debe ser similar a la figura siguiente cuando haya terminado.  
  
5.  Por último, copie el código que aparece en [código HelloData](../../../ado/guide/data/hellodata-code.md)y péguela en la ventana del editor de código del formulario. Presione **F5** para ejecutar el código.  
  
> [!NOTE]
>  En el ejemplo siguiente y a lo largo de la guía, el identificador de usuario "MyId" con la contraseña "123aBc" se usa para autenticarse en el servidor. Debe sustituir estos valores con credenciales de inicio de sesión válido para el servidor. Sustituya también el valor "MySQLServer" con el nombre del servidor.  
  
 Para obtener una descripción detallada del código, consulte [comentarios en HelloData](../../../ado/guide/data/comments-on-hellodata.md).  
  
 ![Muestra Form1 para la aplicación HelloData VB](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|Tipo de control|Property|Valor|  
|------------------|--------------|-----------|  
|Form|NOMBRE|Form1|  
||Alto|6500|  
||Ancho|6500|  
|Cuadrícula de datos de MS|Name|grdDisplay1|  
|TextBox|Name|txtDisplay1|  
||Varias líneas|true|  
|Botón de comando|NOMBRE|cmdGetData|  
||Título|Get Data|  
|Botón de comando|Name|cmdExamineData|  
||Título|Examinar los datos|  
|Botón de comando|NOMBRE|cmdEditData|  
||Título|Editar datos|  
|Botón de comando|NOMBRE|cmdUpdateData|  
||Título|Datos actualizados|
