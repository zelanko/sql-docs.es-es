---
title: Propiedades de canalizaciones con nombre | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a5e2f9b67c74a5eea97209bb812ee2e385c9c41a
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="named-pipes-properties"></a>Propiedades de Canalizaciones con nombre
  Utilice la página **Protocolo**del cuadro de diálogo **Named Pipes Properties** (Propiedades de canalizaciones con nombre) para ver o cambiar la canalización con nombre que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha, cuando se utiliza el protocolo Canalizaciones con nombre.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]debe reiniciarse para habilitar o deshabilitar el protocolo o cambiar la canalización con nombre.  
  
## <a name="options"></a>Opciones  
 **Enabled**  
 Los valores posibles **Yes** y **No**.  
  
 **Nombre de canalización**  
 Especifica la canalización con nombre en la que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha. De manera predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha en: `\\.\pipe\sql\query` para la instancia predeterminada y `\\.\pipe\MSSQL$<instancename>\sql\query` para una instancia con nombre. Este campo tiene un límite de 2.047 caracteres.  
  
## <a name="creating-an-alternate-named-pipe"></a>Crear una canalización con nombre alternativa  
 Para cambiar la canalización con nombre, escriba el nuevo nombre de canalización en el cuadro **Nombre de canalización** y, a continuación, detenga y reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como **sql\query** se conoce ampliamente como la canalización con nombre usada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el cambio de la canalización puede ayudar a reducir el riesgo de ataques por programas malintencionados.  
  
### <a name="example"></a>Ejemplo  
 Escriba **\\\\.\pipe\unit\app** para escuchar en la canalización **unit\app** .  
  
 Escriba **\\\\.\pipe\acct** para escuchar en la canalización **acct** .  
  
## <a name="see-also"></a>Vea también  
 [Habilitar o deshabilitar un protocolo de red de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [Elegir un protocolo de red](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Crear una cadena de conexión válida con canalizaciones con nombre](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)  
  
  

