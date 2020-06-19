---
title: Cómo funcionan los procedimientos almacenados extendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
ms.openlocfilehash: 75082fed6b70c214b4f55b85034ffa371824d24f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027127"
---
# <a name="how-extended-stored-procedures-work"></a>Cómo funcionan los procedimientos almacenados extendidos
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 El procedimiento almacenado extendido funciona del siguiente modo:  
  
1.  Cuando un cliente ejecuta un procedimiento almacenado extendido, la solicitud se transmite en formato de flujo de datos tabular (TDS) o de Protocolo simple de acceso a objetos (SOAP) desde la aplicación cliente a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] busca la DLL asociada al procedimiento almacenado extendido y la carga si no lo está ya.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] llama al procedimiento almacenado extendido solicitado (está implementado como una función dentro de la DLL).  
  
4.  El procedimiento almacenado extendido pasa conjuntos de resultados y devuelve parámetros de retorno al servidor mediante la API Procedimiento almacenado extendido.  
  
## <a name="see-also"></a>Consulte también  
 [Programación de procedimientos almacenados extendidos de motor de base de datos](../database-engine-extended-stored-procedure-programming.md)  
  
  
