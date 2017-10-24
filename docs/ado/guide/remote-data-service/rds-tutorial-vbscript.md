---
title: Tutorial RDS (VBScript) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/14/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6f339f4ce8ab4a0bc536960e63fd53ccbfe08d6b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="rds-tutorial-vbscript"></a>Tutorial RDS (VBScript)
Este es el Tutorial de RDS, escrito en Microsoft Visual Basic Scripting Edition. Para obtener una descripción de la finalidad de este tutorial, vea el [Tutorial de RDS](../../../ado/guide/remote-data-service/rds-tutorial.md).  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 En este tutorial, [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) y [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) se crean en tiempo de diseño, es decir, se definen con etiquetas de objeto, como el siguiente: `<OBJECT>...</OBJECT>`. Como alternativa, se podrían crear en tiempo de ejecución con el [método CreateObject (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md) método. Por ejemplo, el **RDS. DataControl** pudo crear el objeto similar al siguiente:  
  
```  
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
  
## <a name="step-1--specify-a-server-program"></a>Paso 1: Especificar un programa de servidor  
 VBScript puede descubrir el nombre del servidor Web de IIS se está ejecutando en mediante el acceso a VBScript **Request.ServerVariables** método disponible para las páginas Active Server:  
  
```  
"http://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 Sin embargo, para este tutorial, utilice el servidor imaginario "yourServer".  
  
> [!NOTE]
>  Preste atención al tipo de datos de **ByRef** argumentos. VBScript no le permiten especificar el tipo de variable, por lo que siempre se debe pasar un **Variant**. Cuando se utiliza HTTP, RDS permitirá pasar un Variant a un método que espera un valor no Variant si se invoca con el **RDS. DataSpace** objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método. Cuando se utiliza DCOM o un servidor en proceso, debe coincidir con los tipos de parámetros en los lados de cliente y el servidor o recibirá un error "No coinciden los tipos".  
  
```  
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "http://yourServer")  
```  
  
## <a name="step-2a--invoke-the-server-program-with-rdsdatacontrol"></a>Paso 2a: llamar al programa de servidor con RDS. DataControl  
 En este ejemplo es simplemente un comentario que muestra que el comportamiento predeterminado de la **RDS. DataControl** consiste en realizar la consulta especificada.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="http://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b--invoke-the-server-program-with-rdsserverdatafactory"></a>Paso 2b: llamar al programa servidor con RDSServer.DataFactory  
  
## <a name="step-3--server-obtains-a-recordset"></a>Paso 3: El servidor obtiene un conjunto de registros  
  
## <a name="step-4--server-returns-the-recordset"></a>Paso 4: El servidor devuelve el conjunto de registros  
  
```  
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5--datacontrol-is-made-usable-by-visual-controls"></a>Paso 5: DataControl se facilita mediante controles visuales  
  
```  
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a--changes-are-sent-to-the-server-with-rdsdatacontrol"></a>Paso 6a: cambios se envían al servidor con RDS. DataControl  
 En este ejemplo es simplemente un comentario que muestra cómo el **RDS. DataControl** realiza actualizaciones.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="http://yourServer/">  
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
  
## <a name="step-6b--changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>Paso 6b: cambios se envían al servidor con RDSServer.DataFactory  
  
```  
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **Éste es el final del tutorial.**  
  
## <a name="see-also"></a>Vea también  
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   

