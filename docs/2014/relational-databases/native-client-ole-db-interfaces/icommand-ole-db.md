---
title: ICommand (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cdea4400b62906f49c4678494a9ece4fd6e16c8e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111128"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
  Este tema trata el comportamiento de OLE DB que es específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 Insertar datos que sean mayores que el tamaño de una columna suele producir un error. Sin embargo, hay situaciones en las que se devolverá S_OK pero *dwStatus* se configurará en DBSTATUS_S_TRUNCATED. Esto se suele producir al insertar datos con parámetros, donde la columna no es lo bastante grande para contener los datos y no se ha llamado a `ICommandWithParameters::SetParameterInfo`.  
  
## <a name="see-also"></a>Vea también  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  