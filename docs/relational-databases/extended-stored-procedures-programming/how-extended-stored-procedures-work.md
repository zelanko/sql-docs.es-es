---
title: "Cómo funcionan los procedimientos almacenados extendidos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb9c6663cd2891669140c7eb59e44e110f3d5607
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="how-extended-stored-procedures-work"></a>Cómo funcionan los procedimientos almacenados extendidos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, use la integración con CLR.  
  
 El procedimiento almacenado extendido funciona del siguiente modo:  
  
1.  Cuando un cliente ejecuta un procedimiento almacenado extendido, la solicitud se transmite en formato de Protocolo Simple de acceso a objetos (SOAP) de la aplicación cliente o el flujo de datos tabulares (TDS) [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] busca el archivo DLL asociada con el procedimiento almacenado extendido y carga el archivo DLL si ya no está cargado.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] llama el procedimiento almacenado extendido solicitado (se implementa como una función dentro de la DLL).  
  
4.  El procedimiento almacenado extendido pasa conjuntos de resultados y devuelve parámetros de retorno al servidor mediante la API Procedimiento almacenado extendido.  
  
## <a name="see-also"></a>Vea también  
 [Programación de procedimientos almacenados extendidos de motor de base de datos](../../relational-databases/database-engine-extended-stored-procedure-programming.md)  
  
  
