---
title: Registrar y definir entradas de registro en un componente de flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- logs [Integration Services], custom
- custom log entries [Integration Services]
- custom data flow components [Integration Services], logging
- data flow components [Integration Services], logging
ms.assetid: 2190dba9-59b5-480b-b8e9-21d5a54c5917
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e4b328e1e39646f9b47e66bd313940de768ea73c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58386253"
---
# <a name="logging-and-defining-log-entries-in-a-data-flow-component"></a>Registrar y definir entradas de registro en un componente de flujo de datos
  Los componentes de flujo de datos personalizados pueden publicar mensajes en una entrada de registro existente con el método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.PostLogMessage%2A> de la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>. También pueden presentar información al usuario con el método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A> o métodos similares de la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>. Sin embargo, este enfoque supone la sobrecarga de provocar y controlar eventos adicionales y obliga al usuario a buscar los mensajes que le pueden interesar entre todos los mensajes informativos detallados. Puede utilizar una entrada de registro personalizada tal como se describe a continuación para proporcionar información de registro personalizada etiquetada de forma diferenciada a los usuarios del componente.  
  
## <a name="registering-and-using-a-custom-log-entry"></a>Registrar y utilizar una entrada de registro personalizada  
  
### <a name="registering-a-custom-log-entry"></a>Registrar una entrada de registro personalizada  
 Para registrar una entrada de registro personalizada y que la utilice el componente, invalide el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterLogEntries%2A> de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. En el ejemplo siguiente se registra una entrada de registro personalizada y se proporciona un nombre y una descripción.  
  
```csharp  
using Microsoft.SqlServer.Dts.Runtime;  
...  
private const string MyLogEntryName = "My Custom Component Log Entry";  
private const string MyLogEntryDescription = "Log entry from My Custom Component ";  
...  
    public override void RegisterLogEntries()  
    {  
      this.LogEntryInfos.Add(MyLogEntryName,  
        MyLogEntryDescription,  
        Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT);  
    }  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
...  
Private Const MyLogEntryName As String = "My Custom Component Log Entry"   
Private Const MyLogEntryDescription As String = "Log entry from My Custom Component "  
...  
Public  Overrides Sub RegisterLogEntries()   
  Me.LogEntryInfos.Add(MyLogEntryName, _  
    MyLogEntryDescription, _  
    Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT)   
End Sub  
```  
  
 La enumeración <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency> proporciona una sugerencia al motor en tiempo de ejecución sobre la frecuencia con que se registrará el evento:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_OCCASIONAL>: Evento se registra únicamente a veces, no durante cada ejecución.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT>: Evento se registra un número constante de veces durante cada ejecución.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_PROPORTIONAL>: Evento se registra un número de veces proporcionales a la cantidad de trabajo completado.  
  
 En el ejemplo anterior se utiliza <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT> porque el componente espera registrar una entrada una vez por ejecución.  
  
 Después de registrar la entrada de registro personalizada y agregar una instancia del componente personalizado a la superficie del diseñador de flujo de datos, el cuadro de diálogo **Registro** del diseñador muestra una nueva entrada de registro con el nombre "My Custom Component Log Entry" en la lista de entradas de registro disponibles.  
  
### <a name="logging-to-a-custom-log-entry"></a>Registrar en una entrada de registro personalizada  
 Después de registrar la entrada de registro personalizada, el componente puede registrar los mensajes personalizados. En el ejemplo siguiente se escribe una entrada de registro personalizada durante el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> que contiene el texto de una instrucción SQL que utiliza el componente.  
  
```csharp  
public override void PreExecute()  
{  
  DateTime now = DateTime.Now;  
  byte[] additionalData = null;  
  this.ComponentMetaData.PostLogMessage(MyLogEntryName,  
    this.ComponentMetaData.Name,  
    "Command Sent was: " + myCommand.CommandText,  
    now, now, 0, ref additionalData);  
}  
```  
  
```vb  
Public  Overrides Sub PreExecute()   
  Dim now As DateTime = DateTime.Now   
  Dim additionalData As Byte() = Nothing   
  Me.ComponentMetaData.PostLogMessage(MyLogEntryName, _  
    Me.ComponentMetaData.Name, _  
    "Command Sent was: " + myCommand.CommandText, _  
    now, now, 0, additionalData)   
End Sub  
```  
  
 Cuando el usuario ejecuta el paquete, después de seleccionar "My Custom Component Log Entry" en el cuadro de diálogo **Registro**, el registro contendrá una entrada claramente etiquetada como "User::My Custom Component Log Entry". Esta nueva entrada de registro contiene el texto de la instrucción SQL, la marca de tiempo y cualquier dato adicional registrado por el programador.  
  
![Icono de Integration Services (pequeño)](../../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Registro de Integration Services &#40;SSIS&#41;](../../performance/integration-services-ssis-logging.md)  
  
  
