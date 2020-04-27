---
title: Quitar UDT&#39;s con el nombre de los tipos de datos de fecha y hora reservados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- time data type [SQL Server], UDTs
- date data type [SQL Server], UDTs
ms.assetid: 48f109af-b1d1-4f03-a7e3-8a0b05ed94e8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9692bcc5b3c7685e247730b0f203d273f585f1de
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092987"
---
# <a name="remove-udt39s-named-after-the-reserved-date-and-time-data-types"></a>Quitar UDT&#39;s con el nombre de los tipos de datos de fecha y hora reservados
  El Asesor de actualizaciones detectó un tipo definido por el usuario (UDT) que se denomina después de un término reservado para los tipos de datos `date` o `time`.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Los términos usados para los tipos de datos no se deben utilizar como nombres para el Common Language Runtime (CLR) o alias UDTs.  
  
## <a name="corrective-action"></a>Acción correctora  
 Elimine el UDT que se denomina con el tipo de datos y vuelva a crearlo con un nombre no reservado.  
  
  
