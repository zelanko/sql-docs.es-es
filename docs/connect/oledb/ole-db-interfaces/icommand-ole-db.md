---
title: ICommand (OLE DB) | Microsoft Docs
description: Interfaz ICommand (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 9622dfa505fd00bca639d1cfd8919aef4145a85a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790672"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artículo trata el comportamiento de OLE DB que es específico para el controlador OLE DB para SQL Server.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 Insertar datos que sean mayores que el tamaño de una columna suele producir un error. Sin embargo, hay situaciones en las que se devolverá S_OK pero *dwStatus* se configurará en DBSTATUS_S_TRUNCATED. Se suele producir al insertar datos con parámetros, donde la columna no es lo bastante grande para contener los datos y no se ha llamado a **ICommandWithParameters::SetParameterInfo**.  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
