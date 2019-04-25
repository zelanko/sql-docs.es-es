---
title: Cómo funcionan los procedimientos almacenados extendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
ms.openlocfilehash: ab0864e8eb320c63bd757d4c6edab384c6c821b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742241"
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
