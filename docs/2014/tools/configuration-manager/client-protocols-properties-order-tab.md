---
title: Propiedades (pestaña ordenar) los protocolos de cliente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb3055780186c34f6ead494f702874fbc6329f5b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802217"
---
# <a name="client-protocols-properties-order-tab"></a>Propiedades de los protocolos de cliente (pestaña Ordenar)
  Utilice la página **Ordenar**del cuadro de diálogo **Propiedades de los protocolos de cliente** para ver y habilitar los protocolos de cliente.  
  
 Haga clic en un protocolo y, a continuación, haga clic en **Habilitar** o **Deshabilitar** para mover el protocolo seleccionado a la lista **Protocolos deshabilitados** o **Protocolos habilitados** .  
  
 Los protocolos se intentan utilizar en el orden enumerado. Primero se intenta la conexión con el protocolo que está en primer lugar, después con el segundo, etc. Para subir o bajar los protocolos en la lista **Protocolos habilitados**, haga clic en los botones de flecha arriba y flecha abajo. Al conectarse a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un cliente que se encuentre en ese equipo, siempre se intentará utilizar en primer lugar el protocolo **Memoria compartida** si está habilitado.  
  
> [!NOTE]  
>  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient, no se utiliza esta configuración. El orden de los protocolos para .NET SqlClient es primero TCP y, después, las canalizaciones con nombre, que no se pueden modificar.  
  
## <a name="options"></a>Opciones  
 **Protocolos deshabilitados**  
 Muestra una lista de los protocolos que están instalados pero no se utilizan actualmente.  
  
 **Protocolos habilitados**  
 Muestra una lista de los protocolos que están disponibles para los clientes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo.  
  
 **>**  
 Habilita el protocolo que se encuentre resaltado en el cuadro **Protocolos deshabilitados** y lo mueve al cuadro **Protocolos habilitados** .  
  
 **\<**  
 Deshabilita el protocolo que se encuentre resaltado en el cuadro **Protocolos habilitados** y lo mueve al cuadro **Protocolos deshabilitados** .  
  
 Flecha arriba  
 Mueve el protocolo resaltado hacia arriba en la lista. Esto le permite aumentar la prioridad con la que la biblioteca de red intentará utilizar el protocolo seleccionado para las conexiones.  
  
 Flecha abajo  
 Mueve el protocolo resaltado hacia abajo en la lista. Esto le permite reducir la prioridad con la que la biblioteca de red intentará utilizar el protocolo seleccionado para las conexiones.  
  
 **Habilitar el protocolo de memoria compartida**  
 Habilita el protocolo de memoria compartida, que siempre se intenta usar en primer lugar (si está habilitado), al conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un cliente que resida en el equipo.  
  
> [!NOTE]  
>  Si el protocolo se especifica mediante un prefijo o como parte de la cadena de conexión, solo se intenta utilizar el protocolo especificado.  
  
## <a name="see-also"></a>Vea también  
 [Elegir un protocolo de red](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
