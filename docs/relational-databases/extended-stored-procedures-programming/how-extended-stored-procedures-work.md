---
title: Cómo funcionan los procedimientos almacenados extendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 118603088f1cad1ee612f7e4035dc69ba66bc860
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838323"
---
# <a name="how-extended-stored-procedures-work"></a>Cómo funcionan los procedimientos almacenados extendidos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 El procedimiento almacenado extendido funciona del siguiente modo:  
  
1.  Cuando un cliente ejecuta un procedimiento almacenado extendido, la solicitud se transmite en flujo de datos tabulares (TDS) o formato de Protocolo Simple de acceso a objetos (SOAP) de la aplicación cliente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] busca la DLL asociada al procedimiento almacenado extendido y la carga si no lo está ya.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] llama al procedimiento almacenado extendido solicitado (está implementado como una función dentro de la DLL).  
  
4.  El procedimiento almacenado extendido pasa conjuntos de resultados y devuelve parámetros de retorno al servidor mediante la API Procedimiento almacenado extendido.  
  
## <a name="see-also"></a>Vea también  
 [Programación de procedimientos almacenados extendidos de motor de base de datos](../../relational-databases/database-engine-extended-stored-procedure-programming.md)  
  
  
