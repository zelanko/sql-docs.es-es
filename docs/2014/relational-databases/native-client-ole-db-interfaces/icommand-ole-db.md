---
title: ICommand (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 748760817948e71aeb3c2160e63e768b1f0ba54c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707376"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
  Este tema trata el comportamiento de OLE DB que es específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 Insertar datos que sean mayores que el tamaño de una columna suele producir un error. Sin embargo, hay situaciones en las que se devolverá S_OK pero *dwStatus* se configurará en DBSTATUS_S_TRUNCATED. Esto se suele producir al insertar datos con parámetros, donde la columna no es lo bastante grande para contener los datos y no se ha llamado a `ICommandWithParameters::SetParameterInfo`.  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
