---
title: Quitar UDT&#39;s con el nombre del tipo de datos reservado ORDPATH | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 474e910a-6abb-4e28-acc2-055338c011d4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b98fa9765a40d3eb9c05852e9c20c05c4bb818a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856311"
---
# <a name="remove-udt39s-named-after-the-reserved-ordpath-data-type"></a>Quitar UDT&#39;s con el nombre del tipo de datos ORDPATH reservado
  El Asesor de actualizaciones detectó un tipo definido por el usuario (UDT) que se denomina con un término reservado para el tipo de datos `ORDPATH`.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Los términos utilizados para los tipos de datos integrados no se deberían usar como nombres para Common Language Runtime (CLR) o los UDT de alias.  
  
## <a name="corrective-action"></a>Acción correctora  
 Elimine el UDT que se denomina con el tipo de datos y vuelva a crearlo con un nombre no reservado.  
  
## <a name="external-resources"></a>Recursos externos  
 [Crear un tipo definido por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
