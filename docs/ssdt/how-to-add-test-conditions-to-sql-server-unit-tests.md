---
title: Adición de condiciones de prueba a pruebas unitarias de SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 85ba2e56-a0b2-489c-aea2-fb135cce0cfc
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 86e450a6eb6c1e169d5c9dc6147f0ab3cc2a9fb6
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085437"
---
# <a name="how-to-add-test-conditions-to-sql-server-unit-tests"></a>Cómo: Agregar condiciones de prueba a pruebas unitarias de SQL Server
Puede agregar condiciones de prueba a una prueba unitaria de SQL Server mediante el **Diseñador de pruebas unitarias de SQL Server**. Cuando guarda la clase de prueba, las condiciones de prueba se guardan automáticamente en el proyecto de prueba como código de Visual C\# o de Visual Basic en el archivo de código fuente que contiene la clase de prueba. Después de guardar una condición de prueba, puede editarla en el **Diseñador de pruebas unitarias de SQL Server** o en su archivo de código fuente.  
  
### <a name="to-add-test-conditions-to-a-sql-server-unit-test"></a>Para agregar condiciones de prueba a pruebas unitarias de SQL Server  
  
1.  Abra una prueba unitaria de SQL Server en el **Diseñador de pruebas unitarias de SQL Server**.  
  
    El nombre de la prueba que abrió se muestra en la barra de navegación en la parte superior del Diseñador de pruebas unitarias de SQL Server. Mediante la barra de navegación, puede seleccionar los diversos métodos de prueba de la clase de prueba.  
  
2.  En la barra de navegación, haga clic en el método de prueba al que desea agregar condiciones de prueba, o haga clic en **Scripts comunes**.  
  
    > [!NOTE]  
    > Los scripts comunes no pertenecen a una prueba unitaria determinada. Por el contrario, preceden o siguen a las pruebas unitarias de la clase de prueba. Para más información, consulte [Scripts de pruebas unitarias de SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md).  
  
3.  En la barra de navegación, haga clic en el script de Transact\-SQL al que desea agregar condiciones de prueba. Puede agregar condiciones de prueba al script anterior a la prueba, de prueba o posterior a la prueba.  
  
    El script de Transact\-SQL para esa prueba aparece en el editor de Transact\-SQL y las condiciones de prueba aparecen en el panel **Condiciones de prueba**.  
  
4.  En la lista de selección **Condiciones de prueba**, haga clic en una condición de prueba y, a continuación, haga clic en **Agregar condición de prueba** (+).  
  
    La condición de prueba se agrega al método de prueba unitaria.  
  
    > [!NOTE]  
    > Puede reorganizar las condiciones de prueba en un método de prueba si hace clic en una condición de prueba y, a continuación, hace clic en las flechas arriba y abajo en el panel **Condiciones de prueba**.  
  
5.  Seleccione la condición de prueba que acaba de agregar y vea la ventana **Propiedades**.  
  
    Configure la condición de prueba en la ventana Propiedades. Por ejemplo, puede cambiar la propiedad **Tiempo de ejecución** de una condición de prueba de tiempo de ejecución. Si establece esta propiedad, hará que la prueba produzca un error si el script de Transact\-SQL no se ejecuta dentro del tiempo especificado.  
  
## <a name="see-also"></a>Ver también  
[Crear y definir pruebas unitarias de SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Cómo: Crear una prueba unitaria de SQL Server vacía](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
[Cómo: Crear pruebas unitarias de SQL Server para funciones, desencadenadores y procedimientos almacenados](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)  
[Usar condiciones de prueba en pruebas unitarias de SQL Server](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
[Scripts de pruebas unitarias de SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md)  
[Interpretar los resultados de pruebas unitarias de SQL Server](../ssdt/interpreting-sql-server-unit-test-results.md)  
[Cómo: Ejecutar pruebas unitarias de SQL Server](../ssdt/how-to-run-sql-server-unit-tests.md)  
  
