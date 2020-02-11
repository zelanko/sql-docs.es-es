---
title: MSSQLSERVER_7986 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7986 (Database Engine error)
ms.assetid: ae64276c-4e1e-4ef3-9ee9-ebeb2f61e565
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bac8c34542f6c398541e69b690c11d364d37096d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761767"
---
# <a name="mssqlserver_7986"></a>MSSQLSERVER_7986
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|7986|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_PRE_CHECKS_CROSS_OBJECT_LINKAGE|  
|Texto del mensaje|Comprobaciones previas de tabla del sistema: el id. de objeto O_ID tiene encadenamiento entre objetos. La página P_ID1 apunta a P_ID2 en el Id. de unidad de asignación A_ID1 (debería ser A_ID2). Instrucción de comprobación terminada debido a un error irreparable.|  
  
## <a name="explanation"></a>Explicación  
 La primera fase de DBCC CHECKDB es hacer comprobaciones básicas en las páginas de datos de las tablas críticas del sistema. Si se encuentra algún error, no puede repararse; por tanto, DBCC CHECKDB termina inmediatamente. El puntero de página siguiente de la página *P_ID1* en el nivel de datos del objeto especificado apunta a una página, *P_ID2*, de un objeto diferente.  
  
## <a name="user-action"></a>Acción del usuario  
  
### <a name="look-for-hardware-failure"></a>Busque un error de hardware  
 Ejecute un diagnóstico de hardware y corrija cualquier problema. Examine también los registros del sistema y de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows así como el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ver si el error se produjo como resultado de un error de hardware. Arregle cualquier problema relacionado con el hardware que encuentre en estos registros.  
  
 Si sigue teniendo problemas de datos dañados, intente intercambiar diferentes componentes de hardware para aislar el problema. Asegúrese de que el sistema no tiene habilitada la memoria caché de escritura en el controlador de disco. Si cree que el problema se debe a la caché de escritura, póngase en contacto con su proveedor de hardware.  
  
 Finalmente, puede resultarle útil cambiar a un nuevo sistema de hardware. Este cambio puede incluir volver a formatear las unidades de disco y volver a instalar el sistema operativo.  
  
### <a name="restore-from-backup"></a>Restaure mediante la copia de seguridad  
 Si el problema no está relacionado con el hardware y tiene una copia de seguridad limpia disponible, úsela para restaurar la base de datos.  
  
### <a name="run-dbcc-checkdb"></a>Ejecute DBCC CHECKDB  
 No aplicable. Este error no puede repararse automáticamente. Si no puede restaurar la base de datos a partir de una copia de seguridad, póngase en contacto con el servicio de soporte técnico y atención al cliente (CSS) de [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
  
