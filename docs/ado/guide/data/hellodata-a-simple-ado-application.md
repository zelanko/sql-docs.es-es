---
title: "HelloData: Una aplicación ADO Simple | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1c2733381221139373764577df07afa22e40e49
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: Una aplicación ADO Simple
Esta aplicación simple recorre paso a paso cada una de las cuatro operaciones principales de ADO: obtener, examinar, editar y actualizar datos. Estas operaciones se realizan en la base de datos de ejemplo Northwind incluida con Microsoft® SQL Server. Para centrarse en los aspectos básicos de ADO y evitar la acumulación de elementos de código, control de errores en el ejemplo es mínimo.  
  
### <a name="to-run-hellodata"></a>Para ejecutar HelloData  
  
1.  Crear un nuevo proyecto de Visual Basic de EXE estándar que hace referencia a la biblioteca de ADO. Para obtener más información, consulte [que hacen referencia a las bibliotecas de ADO](../../../ado/guide/referencing-the-ado-libraries.md).  
  
2.  Cree cuatro botones de comando en la parte superior del formulario y establezca la **nombre** y **título** propiedades según los valores mostrados en la tabla al final de este tema.  
  
3.  Debajo de los botones, agregue un **Microsoft DataGrid (Control)** (Msdatgrd.ocx). El archivo Msdatgrd.ocx se incluye con Visual Basic y se encuentra en el directorio \windows\system32 o \winnt\system32. Para agregar el control DataGrid a su panel de cuadro de herramientas de Visual Basic, seleccione **componentes...**  desde el **proyecto** menú. A continuación, active la casilla junto a "Microsoft DataGrid Control 6.0 (SP3) (OLEDB)" y, a continuación, haga clic en **Aceptar**. Para agregar el control al proyecto, arrastre el control DataGrid en el cuadro de herramientas al formulario de Visual Basic.  
  
4.  Crear un **cuadro de texto** en el formulario debajo de la cuadrícula y establezca sus propiedades como se muestra en la tabla. El formato debe ser similar a la ilustración siguiente cuando haya terminado.  
  
5.  Por último, copie el código que aparece en [código HelloData](../../../ado/guide/data/hellodata-code.md)y péguela en la ventana del editor de código del formulario. Presione **F5** para ejecutar el código.  
  
> [!NOTE]
>  En el ejemplo siguiente y a lo largo de la guía, el identificador de usuario "MiID" con una contraseña "123aBc" se utiliza para autenticarse en el servidor. Debe sustituir estos valores con credenciales de inicio de sesión válido para el servidor. Además, sustituya el valor de "MySQLServer" con el nombre del servidor.  
  
 Para obtener una descripción detallada del código, consulte [comentarios en HelloData](../../../ado/guide/data/comments-on-hellodata.md).  
  
 ![Muestra Form1 para la aplicación HelloData de VB](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|Tipo de control|Propiedad|Valor|  
|------------------|--------------|-----------|  
|Form|Nombre|Form1|  
||Alto|6500|  
||Ancho|6500|  
|DataGrid MS|Nombre|grdDisplay1|  
|TextBox|Nombre|txtDisplay1|  
||Varias líneas|true|  
|Botón de comando|Nombre|cmdGetData|  
||Título|Get Data|  
|Botón de comando|Nombre|cmdExamineData|  
||Título|Examinar datos|  
|Botón de comando|Nombre|cmdEditData|  
||Título|Editar datos|  
|Botón de comando|Nombre|cmdUpdateData|  
||Título|Datos actualizados|
