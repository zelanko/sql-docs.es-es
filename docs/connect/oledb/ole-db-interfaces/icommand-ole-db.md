---
title: ICommand (OLE DB) | Microsoft Docs
description: Interfaz ICommand (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 2627398879f7525ab8cd9182f2f1102500cfb5a5
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39106211"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artículo trata el comportamiento de OLE DB que es específico para el controlador OLE DB para SQL Server.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 Insertar datos que sean mayores que el tamaño de una columna suele producir un error. Sin embargo, hay situaciones en las que se devolverá S_OK pero *dwStatus* se configurará en DBSTATUS_S_TRUNCATED. Se suele producir al insertar datos con parámetros, donde la columna no es lo bastante grande para contener los datos y no se ha llamado a **ICommandWithParameters::SetParameterInfo**.  
  
## <a name="see-also"></a>Ver también  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
