---
title: Buscar servidores (servidores de redes) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.browseservers.network.f1
ms.assetid: a59ffcd6-4b69-4c5c-9740-699ccb2183fb
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0dfaef0364cf72e994b0fe5de778adc8a18bd715
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="browse-for-servers-network-servers"></a>Buscar servidores (Servidores de redes)
Si se conecta a un componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y no conoce el nombre exacto de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], haga clic en **Buscar más** del cuadro **Nombre del servidor** para abrir el cuadro de diálogo **Buscar servidores**.  
  
Este cuadro de diálogo se rellena con el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en los equipos de servidor. Existen varios motivos por los que es posible que el nombre de una instancia no aparezca en la lista:  
  
-   Es posible que el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no se esté ejecutando en el equipo en el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   El puerto UDP 1434 puede estar bloqueado por un firewall.  
  
-   Es posible que la marca **HideInstance** esté establecida.  
  
Para conectarse a una instancia que no aparece en la lista, escriba una cadena de conexión completa para la instancia, incluido el número de puerto TCP/IP o el nombre de canalización de canalizaciones con nombre.  
  
## <a name="options"></a>Opciones  
**Seleccionar una de las instancias de SQL Server de la red para la conexión**  
Indique el servidor con el que desea conectarse, haciendo clic en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que se muestra en el árbol. Para mostrar u ocultar partes de la vista de árbol, haga clic en los nodos marcados con el símbolo **+** o **–** .  
  

