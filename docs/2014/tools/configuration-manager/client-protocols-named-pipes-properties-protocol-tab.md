---
title: 'Protocolos de cliente: propiedades de canalizaciones con nombre (pestaña Protocolo) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fe7bb05afc8e0814ddb3d872a810759aae2a678
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52746848"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>Protocolos de cliente: Propiedades de Canalizaciones con nombre (pestaña Protocolo)
  En el Administrador de configuración de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilice la pestaña **Protocolo** del cuadro de diálogo **Propiedades de Canalizaciones con nombre** para ver o modificar la descripción de la canalización predeterminada. Para conectarse a una canalización diferente, escriba el nombre de la canalización en el cuadro **Canalización predeterminada** . Para obtener más información sobre cadenas de conexión, vea [Crear una cadena de conexión válida con canalizaciones con nombre](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md).  
  
## <a name="options"></a>Opciones  
 **Canalización predeterminada**  
 Especifica la canalización predeterminada que la biblioteca de red de canalizaciones con nombre utilizará para intentar conectarse a la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha en: `\\.\pipe\sql\query`  
  
 Para conectarse a la canalización predeterminada, escriba `sql\query`  
  
 **Habilitado**  
 Los valores posibles son **Yes** y **No**.  
  
## <a name="see-also"></a>Vea también  
 [Elegir un protocolo de red](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
