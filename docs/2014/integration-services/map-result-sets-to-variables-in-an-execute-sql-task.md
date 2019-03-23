---
title: Asignar conjuntos de resultados a Variables en una tarea Ejecutar SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- mapping result sets to variables [Integration Services]
- variables [Integration Services], mapping result sets to
ms.assetid: f76738b6-dc75-4ff9-a3dd-8b083d8e410e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4c6114fac83862198b37647f6350d657df878ca5
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379643"
---
# <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>Asignar conjuntos de resultados a variables en una tarea Ejecutar SQL
  Este tema describe cómo crear una asignación entre un conjunto de resultados y una variable en una tarea Ejecutar SQL. La asignación de un conjunto de resultados a una variable hace que el conjunto de resultados esté disponible para otros elementos del paquete. Por ejemplo, un script de la tarea Script puede leer la variable y luego utilizar los valores del conjunto de resultados, o un origen XML puede consumir el conjunto de resultados almacenados en una variable. Si un paquete primario genera el conjunto de resultados, este conjunto de resultados se puede poner a disposición de un paquete secundario llamado por la tarea Ejecutar paquete asignando el conjunto de resultados a una variable del paquete primario, y luego creando una configuración de variable de paquete primario en el paquete secundario a fin de almacenar el valor de la variable primaria.  
  
 Para obtener descripciones de los diferentes tipos de conjuntos de resultados y los tipos de datos de variables que se pueden asignar a conjuntos de resultados, vea [Conjuntos de resultados en la tarea Ejecutar SQL](control-flow/execute-sql-task.md).  
  
### <a name="to-map-a-result-set-to-a-variable"></a>Para asignar un conjunto de resultados a una variable  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el **Explorador de soluciones**, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Si el paquete no incluye en ese momento una tarea Ejecutar SQL, agregue una al flujo de control del paquete. Para obtener más información, consulte [agregar o eliminar una tarea o un contenedor en un flujo de Control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
5.  Haga doble clic en la tarea Ejecutar SQL.  
  
6.  En el cuadro de diálogo **Editor de la tarea Ejecutar SQL** , en la página **General** , seleccione el tipo de conjunto de resultados **Fila única**, **Conjunto de resultados completo**o **XML** .  
  
     Para obtener descripciones de los distintos conjuntos de resultados, vea [Conjuntos de resultados en la tarea Ejecutar SQL](result-sets-in-the-execute-sql-task.md)  
  
7.  Haga clic en **Conjunto de resultados**.  
  
8.  Para agregar una asignación de conjunto de resultados, haga clic en **Agregar**.  
  
9. En la lista **Nombre de variable** , seleccione una variable o cree una variable nueva. Para más información, vea [Agregar, eliminar, cambiar el ámbito de la variable definida por el usuario en un paquete](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md).  
  
     Para obtener descripciones de los tipos de datos de variables que se pueden asignar a los distintos conjuntos de resultados, vea [Conjuntos de resultados en la tarea Ejecutar SQL](result-sets-in-the-execute-sql-task.md).  
  
     Para obtener información sobre cómo asignar una variable a una sola columna y cómo asignar varias variables a varias columnas, vea la sección **Llenar una variable con un conjunto de resultados** de [Result Sets in the Execute SQL Task](control-flow/execute-sql-task.md).  
  
10. En la lista **Nombre del resultado** , opcionalmente, modifique el nombre del conjunto de resultados.  
  
     En general, puede usar el nombre de columna como nombre del conjunto de resultados, o puede usar la posición ordinal de la columna en la lista de columnas como conjunto de resultados. La posibilidad de usar un nombre de columna como el nombre del conjunto de resultados depende del proveedor para el que se haya configurado la tarea. No todos los proveedores ponen los nombres de columna a disposición.  
  
11. Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Tarea Ejecutar SQL](control-flow/execute-sql-task.md)   
 [Conjuntos de resultados en la tarea Ejecutar SQL](result-sets-in-the-execute-sql-task.md)   
 [Tarea Ejecutar paquete](control-flow/execute-package-task.md)   
 [Configuraciones de paquetes](../../2014/integration-services/package-configurations.md)   
 [Crear configuraciones de paquetes](../../2014/integration-services/create-package-configurations.md)   
 [Use los valores de Variables y parámetros de un paquete secundario](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)   
 [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
  
