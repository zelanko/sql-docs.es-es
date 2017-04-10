---
title: "Protocolos de cliente: Propiedades de Canalizaciones con nombre (pesta&#241;a Protocolo) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "canalizaciones [SQL Server], conectarse a"
  - "Canalizaciones con nombre [SQL Server], canalización predeterminada"
  - "protocolos de cliente [SQL Server]"
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Protocolos de cliente: Propiedades de Canalizaciones con nombre (pesta&#241;a Protocolo)
  En el Administrador de configuración de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilice la pestaña **Protocolo** del cuadro de diálogo **Propiedades de Canalizaciones con nombre** para ver o modificar la descripción de la canalización predeterminada. Para conectarse a una canalización diferente, escriba el nombre de la canalización en el cuadro **Canalización predeterminada** . Para obtener más información sobre cadenas de conexión, vea [Creating a Valid Connection String Using Named Pipes](../Topic/Creating%20a%20Valid%20Connection%20String%20Using%20Named%20Pipes.md).  
  
## Opciones  
 **Canalización predeterminada**  
 Especifica la canalización predeterminada que la biblioteca de red de canalizaciones con nombre utilizará para intentar conectarse a la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha en: `\\.\pipe\sql\query`  
  
 Para conectarse a la canalización predeterminada, escriba `sql\query`  
  
 **Habilitado**  
 Los valores posibles son **Yes** y **No**.  
  
## Vea también  
 [Elegir un protocolo de red](../Topic/Choosing%20a%20Network%20Protocol.md)  
  
  