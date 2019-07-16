---
title: Crear casos de prueba (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: b3f54a38ae995dd2c83fd36647393f81b802fde2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948453"
---
# <a name="creating-test-cases-sybasetosql"></a>Creación de casos de prueba (SybaseToSQL)
Use el Asistente de caso de prueba para crear una prueba. Este asistente le permite crear casos de prueba eligiendo probados y comprobados los objetos y especificando los parámetros de pruebas.  
  
## <a name="starting-the-test-case-wizard"></a>Para iniciar al Asistente de caso de prueba  
Para iniciar el Asistente de caso de prueba, haga clic **nuevo caso de prueba...**  desde el **evaluador** menú.  
  
Cuando se inicia, el asistente busca ssmatester2005db de base de datos o ssmatester2008db (según el tipo de proyecto) del servidor de origen Sybase. Es el esquema de extensión evaluador utilizado para almacenar los objetos auxiliares. Si el Asistente de caso de prueba no se encuentra ssmatester2005db o ssmatester2008db, muestra una ventana de cuadro de diálogo que propone para crear la base de datos de extensión de evaluador. (Esta situación suele sucede durante la primera ejecución del evaluador de SSMA.)  
  
Si aparece el cuadro de diálogo, haga clic en **Sí** para crear la base de datos de Sybase evaluador en el servidor de origen. A continuación, una nueva ventana del cuadro de diálogo aparecerá en el que debe agregar uno o varios dispositivos en los que se va a buscar la nueva base de datos de la herramienta de comprobación. Haga clic en **agregar** para agregar un dispositivo. En el **asignación de espacio de base de datos de evaluador** cuadro de diálogo Elegir el dispositivo y especifique el tamaño de la base de datos de evaluador. Además, puede establecer el dispositivo para los registros de la base de datos independiente. Tenga en cuenta que debe tener privilegios de Sybase para crear bases de datos.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Información general de la creación de casos de prueba mediante el Asistente  
El proceso de creación de un caso de prueba consta de cinco pasos:  
  
1.  [Inicialización de casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md).  
  
2.  [Selección y configuración de objetos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md).  
  
3.  [Selección y configuración de los objetos afectados &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md).  
  
4.  [Personalización del orden de las llamadas &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md).  
  
5.  [Finalización de la preparación del caso de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md).  
  
## <a name="see-also"></a>Vea también  
[Pruebas con objetos de base de datos migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
