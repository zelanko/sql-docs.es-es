---
title: Eliminación de una tabla de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- SQL Server Native Client OLE DB provider, tables
- removing tables
- dropping tables
ms.assetid: b6d6c4de-43c6-473e-92aa-34ffddd58cbe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6f005b9ab1c3d334242b2a20d47f6e4646d6cef8
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704546"
---
# <a name="dropping-a-sql-server-table"></a>Quitar una tabla de SQL Server
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client expone la función **ITableDefinition::D roptable** . Esto permite a los consumidores quitar una [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla de una base de datos.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
## <a name="see-also"></a>Consulte también  
 [Tablas e índices](tables-and-indexes.md)  
  
  
