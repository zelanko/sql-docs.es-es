---
title: Crear casos de prueba (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: a2c1bd3fea167a784d86f7e323566f73c3a01f86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287712"
---
# <a name="creating-test-cases-oracletosql"></a>Creación de casos de prueba (OracleToSQL)
Use el Asistente de caso de prueba para crear una prueba. Este asistente le permite crear casos de prueba eligiendo probados y comprobados los objetos y especificando los parámetros de pruebas.  
  
## <a name="starting-the-test-case-wizard"></a>Para iniciar al Asistente de caso de prueba  
Para iniciar el Asistente de caso de prueba, haga clic **nuevo caso de prueba...**  desde el **evaluador** menú.  
  
Cuando se inicia, el asistente busca el esquema SSMATESTER_ORACLE en el servidor de Oracle de origen. Es el esquema de extensión evaluador utilizado para almacenar los objetos auxiliares. Si el Asistente de caso de prueba no se encuentra SSMATESTER_ORACLE, muestra una ventana de cuadro de diálogo que propone para crear el esquema. (Esta situación suele sucede durante la primera ejecución del evaluador de SSMA.)  
  
Si aparece el cuadro de diálogo, haga clic en **Sí** para crear el esquema SSMATESTER_ORACLE en el servidor de origen. Tenga en cuenta que debe tener privilegios de Oracle para crear un nuevo usuario y crear objetos en el esquema de este usuario.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Información general de la creación de casos de prueba mediante el Asistente  
El proceso de creación de un caso de prueba consta de cinco pasos:  
  
1.  [Inicialización de casos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [Selección y configuración de objetos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [Selección y configuración de los objetos afectados &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [Personalización del orden de las llamadas &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [Finalización de la preparación del caso de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>Vea también  
[Pruebas con objetos de base de datos migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
