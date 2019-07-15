---
title: 'Protocolos de cliente: propiedades de canalizaciones con nombre (pestaña Protocolo) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 1b7b2ce455571b5c588db86b3df6f469dd930e11
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732865"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>Protocolos de cliente: Propiedades de Canalizaciones con nombre (pestaña Protocolo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  En el Administrador de configuración de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilice la pestaña **Protocolo** del cuadro de diálogo **Propiedades de Canalizaciones con nombre** para ver o modificar la descripción de la canalización predeterminada. Para conectarse a una canalización diferente, escriba el nombre de la canalización en el cuadro **Canalización predeterminada** . Para obtener más información sobre cadenas de conexión, vea [Creating a Valid Connection String Using Named Pipes](https://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f).  
  
## <a name="options"></a>Opciones  
 **Canalización predeterminada**  
 Especifica la canalización predeterminada que la biblioteca de red de canalizaciones con nombre utilizará para intentar conectarse a la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha en: `\\.\pipe\sql\query`  
  
 Para conectarse a la canalización predeterminada, escriba `sql\query`  
  
 **Habilitado**  
 Los valores posibles son **Yes** y **No**.  
  
## <a name="see-also"></a>Consulte también  
 [Elegir un protocolo de red](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
