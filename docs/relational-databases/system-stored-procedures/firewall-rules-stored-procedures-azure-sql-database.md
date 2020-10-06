---
description: Procedimientos almacenados de reglas de Firewall (Azure SQL Database)
title: Procedimientos almacenados para las reglas del firewall
titleSuffix: Azure SQL Database
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- firewall rules stored procedures
- firewall_rules, setting
- firewall_rules, Azure SQL Database
- firewall systems, Azure SQL Database
ms.assetid: 3d4c2585-00de-46b5-8eee-0efb71cb3aea
author: VanMSFT
ms.author: vanto
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e6a14687e8210133e2a80c0f678aebe7c9b31194
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753823"
---
# <a name="firewall-rules-stored-procedures-azure-sql-database"></a>Procedimientos almacenados de reglas de Firewall (Azure SQL Database)
[!INCLUDE [asdb-asa](../../includes/applies-to-version/asdb-asa.md)]

  Esta sección contiene los siguientes procedimientos almacenados que establecen o eliminan reglas de firewall. [!INCLUDE[tsql_md](../../includes/tsql-md.md)] las reglas de Firewall se pueden usar con [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] . Para obtener más información, consulte [configuración de reglas de Firewall de Azure SQL Database: Introducción](/azure/azure-sql/database/firewall-configure).

:::row:::
    :::column:::
        [sp_set_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)
    :::column-end:::
    :::column:::
        [sp_delete_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_set_database_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)
    :::column-end:::
    :::column:::
        [sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)
    :::column-end:::
:::row-end:::

&nbsp;
  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , use las reglas de Firewall de Windows. Para más información, vea [Configurar Firewall de Windows para el acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).   
