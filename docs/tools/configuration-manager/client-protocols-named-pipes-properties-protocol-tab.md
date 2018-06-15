---
title: 'Protocolos de cliente: propiedades de canalizaciones con nombre (pestaña Protocolo) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77ed1042003fb41fa22bd2a74c0f73ff0d85a1ae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33067742"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>Protocolos de cliente: Propiedades de Canalizaciones con nombre (pestaña Protocolo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  En el Administrador de configuración de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilice la pestaña **Protocolo** del cuadro de diálogo **Propiedades de Canalizaciones con nombre** para ver o modificar la descripción de la canalización predeterminada. Para conectarse a una canalización diferente, escriba el nombre de la canalización en el cuadro **Canalización predeterminada** . Para obtener más información sobre cadenas de conexión, vea [Creating a Valid Connection String Using Named Pipes](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f).  
  
## <a name="options"></a>Opciones  
 **Canalización predeterminada**  
 Especifica la canalización predeterminada que la biblioteca de red de canalizaciones con nombre utilizará para intentar conectarse a la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha en: `\\.\pipe\sql\query`  
  
 Para conectarse a la canalización predeterminada, escriba `sql\query`  
  
 **Habilitado**  
 Los valores posibles son **Yes** y **No**.  
  
## <a name="see-also"></a>Ver también  
 [Elegir un protocolo de red](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
