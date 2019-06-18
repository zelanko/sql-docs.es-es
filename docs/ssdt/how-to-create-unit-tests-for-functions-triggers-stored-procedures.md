---
title: 'Procedimientos: Crear pruebas unitarias de SQL Server para funciones, desencadenadores y procedimientos almacenados | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: bda57c10-a1ab-4a1a-8a71-42085a3cb793
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5d985e2b2638d8b0047f5b4d010d87c8f631af65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090223"
---
# <a name="how-to-create-sql-server-unit-tests-for-functions-triggers-and-stored-procedures"></a>Procedimientos: Creación de pruebas unitarias de SQL Server para funciones, desencadenadores y procedimientos almacenados
Puede escribir pruebas unitarias que evalúen los cambios en cualquier objeto de base de datos. Sin embargo, SQL Server Data Tools incluye compatibilidad adicional para crear pruebas para funciones de base de datos, desencadenadores y procedimientos almacenados de un nodo de proyecto de base de datos del Explorador de objetos de SQL Server. El código auxiliar de Transact\-SQL puede generarse automáticamente para que pueda personalizarlo.  
  
### <a name="to-create-a-sql-server-unit-test-from-a-function-trigger-or-stored-procedure"></a>Para crear una prueba unitaria de SQL Server a partir de una función, un desencadenador o un procedimiento almacenado  
  
1.  Vea [Tutorial: Crear y ejecutar una prueba unitaria de SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md) para obtener un ejemplo de cómo agregar una prueba unitaria a un procedimiento almacenado en la sección "Para crear una prueba unitaria de SQL Server para los procedimientos almacenados".  
  
    La condición de prueba no concluyente es la condición predeterminada que se agrega a cada prueba. Esta condición de prueba se incluye para indicar que la comprobación de la prueba no se ha implementado. Elimine esta condición de la prueba después de agregar otras condiciones de prueba. Para más información, vea: [Cómo: Incorporar condiciones de prueba a pruebas unitarias de SQL Server](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md).  
  
## <a name="see-also"></a>Consulte también  
[Crear y definir pruebas unitarias de SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Cómo: Crear una prueba unitaria de SQL Server vacía](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
  
