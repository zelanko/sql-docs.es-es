---
title: Creación de pruebas unitarias de SQL Server para funciones, desencadenadores y procedimientos almacenados | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bda57c10-a1ab-4a1a-8a71-42085a3cb793
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96676bfa7c997d94eb79712f67b4b51fd165134b
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082607"
---
# <a name="how-to-create-sql-server-unit-tests-for-functions-triggers-and-stored-procedures"></a>Cómo: Crear pruebas unitarias de SQL Server para funciones, desencadenadores y procedimientos almacenados
Puede escribir pruebas unitarias que evalúen los cambios en cualquier objeto de base de datos. Sin embargo, SQL Server Data Tools incluye compatibilidad adicional para crear pruebas para funciones de base de datos, desencadenadores y procedimientos almacenados de un nodo de proyecto de base de datos del Explorador de objetos de SQL Server. El código auxiliar de Transact\-SQL puede generarse automáticamente para que pueda personalizarlo.  
  
### <a name="to-create-a-sql-server-unit-test-from-a-function-trigger-or-stored-procedure"></a>Para crear una prueba unitaria de SQL Server a partir de una función, un desencadenador o un procedimiento almacenado  
  
1.  Consulte [Tutorial: Crear y ejecutar una prueba unitaria de SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md) para obtener un ejemplo de cómo agregar una prueba unitaria a un procedimiento almacenado en la sección "Para crear una prueba unitaria de SQL Server para los procedimientos almacenados".  
  
    La condición de prueba no concluyente es la condición predeterminada que se agrega a cada prueba. Esta condición de prueba se incluye para indicar que la comprobación de la prueba no se ha implementado. Elimine esta condición de la prueba después de agregar otras condiciones de prueba. Para más información, consulte [Cómo: Agregar condiciones de prueba a pruebas unitarias de SQL Server](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md).  
  
## <a name="see-also"></a>Ver también  
[Crear y definir pruebas unitarias de SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Cómo: Crear una prueba unitaria de SQL Server vacía](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
  
