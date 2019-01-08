---
title: Tutorial de RDS (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a50b9d8c1f22f23f3533240b2543ef981fef8e9
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535198"
---
# <a name="rds-tutorial-vbscript"></a>Tutorial de RDS (VBScript)
Este es el Tutorial de RDS, escrito en Microsoft Visual Basic Scripting Edition. Para obtener una descripción del propósito de este tutorial, vea el [Tutorial de RDS](../../../ado/guide/remote-data-service/rds-tutorial.md).  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 En este tutorial, [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) y [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) se crean en tiempo de diseño: es decir, se definen con etiquetas de objeto similar al siguiente: `<OBJECT>...</OBJECT>`. Como alternativa, podría crearse en tiempo de ejecución con el [método CreateObject (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md) método. Por ejemplo, el **RDS. DataControl** se pudo crear el objeto similar al siguiente:  
  
```vb
Set DC = Server.CreateObject("RDS.DataControl")  
   <!-- RDS.DataControl -->  
   <OBJECT   
      ID="DC1" CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E33">  
   </OBJECT>  
  
   <!-- RDS.DataSpace -->  
   <OBJECT   
      ID="DS1" WIDTH=1 HEIGHT=1  
      CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
   </OBJECT>  
  
   <SCRIPT LANGUAGE="VBScript">  
  
   Sub RDSTutorial()  
   Dim DF1   
```  
  
## <a name="step-1---specify-a-server-program"></a>Paso 1: especificar un programa de servidor  
 VBScript puede detectar el nombre del servidor Web de IIS se está ejecutando mediante el acceso a VBScript **Request.ServerVariables** método disponible para las páginas Active Server:  
  
```vb
"https://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 Sin embargo, para este tutorial, utilice el servidor imaginario "yourServer".  
  
> [!NOTE]
>  Preste atención al tipo de datos de **ByRef** argumentos. VBScript no le permiten especificar el tipo de variable, por lo que siempre se debe pasar un **Variant**. Cuando se utiliza HTTP, RDS permitirá pasar un tipo Variant a un método que espera un valor no Variant si se invoca con el **RDS. DataSpace** objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método. Cuando se utiliza DCOM o un servidor en proceso, debe coincidir con los tipos de parámetros en los lados cliente y servidor o recibirá un error "No coinciden los tipos".  
  
```vb
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "https://yourServer")  
```  
  
## <a name="step-2a---invoke-the-server-program-with-rdsdatacontrol"></a>Paso 2a: llamar al programa de servidor con RDS. Control de datos  
 En este ejemplo es simplemente un comentario que muestra que el comportamiento predeterminado de la **RDS. DataControl** consiste en realizar la consulta especificada.  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b---invoke-the-server-program-with-rdsserverdatafactory"></a>Paso 2b: llamar al programa de servidor con RDSServer.DataFactory  
  
## <a name="step-3---server-obtains-a-recordset"></a>Paso 3: servidor obtiene un conjunto de registros  
  
## <a name="step-4---server-returns-the-recordset"></a>Paso 4: devuelve el conjunto de registros de servidor  
  
```vb
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5---datacontrol-is-made-usable-by-visual-controls"></a>Paso 5: DataControl se facilita mediante controles visuales  
  
```vb
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a---changes-are-sent-to-the-server-with-rdsdatacontrol"></a>El paso 6a: los cambios se envían al servidor con RDS. Control de datos  
 En este ejemplo es simplemente un comentario que muestra cómo el **RDS. DataControl** realiza las actualizaciones.  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial6A()  
Dim RS  
DC1.Refresh  
...  
Set RS = DC1.Recordset  
' Edit the Recordset object...  
' The SERVER and CONNECT properties are already set from Step 2A.  
Set DC1.SourceRecordset = RS  
...  
DC1.SubmitChanges  
```  
  
## <a name="step-6b---changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>Paso 6b: los cambios se envían al servidor con RDSServer.DataFactory  
  
```vb
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **Éste es el final del tutorial.**  
  
## <a name="see-also"></a>Vea también  
 [Tutorial de RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
