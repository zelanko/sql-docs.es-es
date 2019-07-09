---
title: Desconectar usuarios y sesiones en Analysis Services Server | Microsoft Docs
ms.date: 07/05/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 696c6548dadda2412566acf7fae1e2cff2b28095
ms.sourcegitcommit: 9af07bd57b76a34d3447e9e15f8bd3b17709140a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624396"
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>Desconectar usuarios y sesiones en el servidor de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]
  Como administrador, es posible que desee como parte de la administración de cargas de trabajo de la actividad del usuario final. Esto se lleva a cabo cancelando sesiones y conexiones. Las sesiones se pueden formar automáticamente cuando se ejecuta una consulta (implícito) o definirse en el momento en que las crea el administrador (explícito). Las conexiones son conductos abiertos con los que se pueden ejecutar las consultas. Tanto las sesiones como las conexiones se pueden terminar aunque estén activas. Por ejemplo, desea finalizar el procesamiento de una sesión si el procesamiento está tardando demasiado o si han surgido dudas sobre si el comando que se está ejecutando está correctamente escrito.  
  
## <a name="ending-sessions-and-connections"></a>Terminar sesiones y conexiones  
 Para administrar sesiones y conexiones, utilice las vistas de administración dinámica (DMV) y XMLA:  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia de Analysis Services.  
  
2.  Pegue una de las siguientes consultas de DMV en una ventana de consulta MDX para obtener una lista de todas las sesiones, conexiones y comandos que se están ejecutando actualmente:  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  (Esta consulta no se aplica a Azure Analysis Services)
  
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

Cancelar un SessionID o SPID se cancelarán los comandos activos que se ejecutan en la sesión correspondiente a la SessionID o SPID. Cancelación de una conexión identificará la sesión asociada a la conexión y cancelar los comandos activos que se ejecutan en esa sesión. En raras ocasiones, no se cierra una conexión si el motor no puede realizar un seguimiento de todas las sesiones y SPID asociados con la conexión; Por ejemplo, cuando varias sesiones están abiertas en un escenario HTTP.   
  
Para más información sobre el XMLA al que hace referencia en este tema, consulte [Ejecutar método &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) y [Cancelar elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla).  
  
## <a name="see-also"></a>Vea también  
 [Administrar conexiones y sesiones &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Elemento BeginSession &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/beginsession-element-xmla)   
 [EndSession, elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/endsession-element-xmla)   
 [Session, elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/session-element-xmla)  
  
  
