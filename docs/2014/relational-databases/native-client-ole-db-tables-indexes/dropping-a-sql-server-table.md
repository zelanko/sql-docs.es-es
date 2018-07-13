---
title: Quitar una tabla SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- SQL Server Native Client OLE DB provider, tables
- removing tables
- dropping tables
ms.assetid: b6d6c4de-43c6-473e-92aa-34ffddd58cbe
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6bb2446d395b7c913653f7ac70805c5b0c5c050
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408973"
---
# <a name="dropping-a-sql-server-table"></a>Quitar una tabla de SQL Server
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **ITableDefinition:: Droptable** función. Esto permite que los consumidores puedan quitar una [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla a partir de una base de datos.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el *pwszName* miembro de la *uName* union en la *pTableID* parámetro. El *eKind* miembro de *pTableID* debe ser DBKIND_NAME.  
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](tables-and-indexes.md)  
  
  
