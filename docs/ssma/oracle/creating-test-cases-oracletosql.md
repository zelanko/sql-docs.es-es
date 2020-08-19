---
description: Creación de casos de prueba (OracleToSQL)
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
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 4f7183089fd67f413515034a557e4b73388f950f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418391"
---
# <a name="creating-test-cases-oracletosql"></a>Creación de casos de prueba (OracleToSQL)
Use el Asistente para casos de prueba para crear una prueba. Este asistente le permite crear casos de prueba eligiendo objetos comprobados y comprobados y especificando los parámetros de prueba.  
  
## <a name="starting-the-test-case-wizard"></a>Iniciar el Asistente para casos de prueba  
Para iniciar el Asistente para casos de prueba, haga clic en **nuevo caso de prueba...** en el menú de **evaluador** .  
  
Cuando se inicia, el asistente busca SSMATESTER_ORACLE de esquema en el servidor de Oracle de origen. Es el esquema de la extensión de evaluador que se usa para almacenar objetos auxiliares. Si el Asistente para casos de prueba no encuentra SSMATESTER_ORACLE, muestra una ventana de cuadro de diálogo que propone crear el esquema. (Normalmente, esta situación se produce durante la primera ejecución de la herramienta SSMA Tester).  
  
Si obtiene la ventana del cuadro de diálogo, haga clic en **sí** para crear SSMATESTER_ORACLE esquema en el servidor de origen. Tenga en cuenta que debe tener privilegios de Oracle para crear un nuevo usuario y crear objetos en el esquema de este usuario.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Información general sobre la creación de casos de prueba mediante el asistente  
El proceso de creación de un caso de prueba consta de cinco pasos:  
  
1.  [Inicializar casos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [Seleccionar y configurar objetos para probar &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [Seleccionar y configurar objetos afectados &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [Personalizar el orden de llamadas &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [Finalizando la preparación del caso de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>Consulte también  
[Probar objetos de base de datos migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
