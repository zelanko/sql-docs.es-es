---
title: Quitar UDT&#39;s con nombre del tipo de datos ORDPATH reservado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 474e910a-6abb-4e28-acc2-055338c011d4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3ee155c70a8b10d4437d6b2f374c8b9497bf3faa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092922"
---
# <a name="remove-udt39s-named-after-the-reserved-ordpath-data-type"></a>Quitar UDT&#39;s con nombre del tipo de datos Reserved ORDPATH
  El Asesor de actualizaciones detectó un tipo definido por el usuario (UDT) que se denomina con un término reservado para el tipo de datos `ORDPATH`.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Los términos utilizados para los tipos de datos integrados no se deberían usar como nombres para Common Language Runtime (CLR) o los UDT de alias.  
  
## <a name="corrective-action"></a>Acción correctora  
 Elimine el UDT que se denomina con el tipo de datos y vuelva a crearlo con un nombre no reservado.  
  
## <a name="external-resources"></a>Recursos externos  
 [Crear un tipo definido por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
