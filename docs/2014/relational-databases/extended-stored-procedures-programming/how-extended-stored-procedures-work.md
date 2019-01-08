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
manager: craigg
ms.openlocfilehash: 9b52e8fd5cda7d0b05ebbddbb422f74bd81b1993
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804117"
---
# <a name="how-extended-stored-procedures-work"></a>Cómo funcionan los procedimientos almacenados extendidos
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 El procedimiento almacenado extendido funciona del siguiente modo:  
  
1.  Cuando un cliente ejecuta un procedimiento almacenado extendido, la solicitud se transmite en flujo de datos tabulares (TDS) o formato de Protocolo Simple de acceso a objetos (SOAP) de la aplicación cliente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] busca la DLL asociada al procedimiento almacenado extendido y la carga si no lo está ya.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] llama al procedimiento almacenado extendido solicitado (está implementado como una función dentro de la DLL).  
  
4.  El procedimiento almacenado extendido pasa conjuntos de resultados y devuelve parámetros de retorno al servidor mediante la API Procedimiento almacenado extendido.  
  
## <a name="see-also"></a>Vea también  
 [Programación de procedimientos almacenados extendidos de motor de base de datos](../database-engine-extended-stored-procedure-programming.md)  
  
  
