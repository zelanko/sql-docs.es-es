---
title: Desconectar usuarios y sesiones en Analysis Services Server | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: da6f41a06097af6e386b940804be2563fc287c80
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>Desconectar usuarios y sesiones en el servidor de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Como administrador de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede que desee la actividad del usuario final como parte de la administración de la carga de trabajo. Esto se lleva a cabo cancelando sesiones y conexiones. Las sesiones se pueden formar automáticamente cuando se ejecuta una consulta (implícito) o definirse en el momento en que las crea el administrador (explícito). Las conexiones son conductos abiertos con los que se pueden ejecutar las consultas. Tanto las sesiones como las conexiones se pueden terminar aunque estén activas. Por ejemplo, es posible que un administrador desee finalizar el procesamiento de una sesión si dicho procesamiento está tardando demasiado o si han surgido dudas sobre si el comando que se está ejecutando está correctamente escrito.  
  
## <a name="ending-sessions-and-connections"></a>Terminar sesiones y conexiones  
 Para administrar sesiones y conexiones, puede utilizar las vistas de administración dinámica (DMV) y XMLA:  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia de Analysis Services.  
  
2.  Pegue una de las siguientes consultas de DMV en una ventana de consulta MDX para obtener una lista de todas las sesiones, conexiones y comandos que se están ejecutando actualmente:  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  
  
     `Select * from $System.Discover_Commands`  
  
3.  Presione F5 para ejecutar la consulta.  
  
     La consulta de DMV devuelve información de conexión y de sesión en un conjunto de resultados tabulares cuya lectura y copia es más fácil.  
  
 Mantenga la ventana de consulta abierta. En el paso siguiente, querrá volver a esta página para copiar los SPID de la sesión que desea desconectar.  
  
 Para terminar una sesión, abra una segunda ventana de consulta XMLA.  
  
1.  Pegue la siguiente sintaxis en una ventana de consulta MDX, reemplazando el marcador de posición ConnectionID, SessionID o SPID con un valor válido que copió en el paso anterior.  
  
    ```  
    <Cancel xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  
       <ConnectionID>111</ConnectionID>  
       <SessionID>222</SessionID>  
       <SPID>333</SPID>  
  
    <CancelAssociated>1</CancelAssociated>  
    </Cancel>  
  
    ```  
  
2.  Presione F5 para ejecutar el comando de cancelación.  
  
 La finalización de una conexión cancela todas las sesiones y SPID, cerrando la sesión del host.  
  
 La finalización de una sesión detiene todos los comandos (SPID) que se estén ejecutando como parte de dicha sesión.  
  
 La finalización de un SPID cancela un comando concreto.  
  
 En muy pocos casos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no cerrará una conexión si no puede realizar el seguimiento de todas las sesiones y SPID asociados a la conexión (por ejemplo, cuando haya varias sesiones abiertas en un escenario HTTP).  
  
 Para obtener más información sobre el XMLA al que se hace referencia en este tema, vea [Método Execute &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md) y [Elemento Cancel &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Administrar las conexiones y sesiones & #40; XMLA & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Elemento BeginSession & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)   
 [EndSession, elemento & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Elemento de sesión & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)  
  
  
