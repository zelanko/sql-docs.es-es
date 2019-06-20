---
title: Consultas de Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0b4323715155ddb433012624f9d7a5df9bb0a29c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767667"
---
# <a name="integration-services-ssis-queries"></a>Consultas de Integration Services (SSIS)
  La tarea Ejecutar SQL, el origen de OLE DB, el destino de OLE DB y la transformación Búsqueda pueden utilizar consultas de SQL. En la tarea Ejecutar SQL, las instrucciones SQL pueden crear, actualizar y eliminar datos y objetos de bases de datos, ejecutar procedimientos almacenados y ejecutar instrucciones SELECT. En el origen de OLE DB y la transformación Búsqueda, las instrucciones SQL son normalmente instrucciones SELECT o EXEC. Normalmente, éstas últimas ejecutan procedimientos almacenados que devuelven conjuntos de resultados.  
  
 Una consulta se puede analizar para ver si es válida. Al analizar una consulta que usa una conexión a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], la consulta se analiza, se ejecuta y el resultado de la ejecución (correcta o errónea) se asigna al resultado del análisis. Si la consulta utiliza una conexión a datos que no sean de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], la instrucción solo se analiza.  
  
 La instrucción SQL se puede definir introduciéndola directamente en el diseñador, o especificando una conexión de archivos o una variable que contenga la instrucción.  
  
## <a name="direct-input-sql"></a>Entrada directa en SQL  
 El Generador de consultas está disponible en la interfaz de usuario de la tarea Ejecutar SQL, el origen de OLE DB, el destino de OLE DB y la transformación Búsqueda. El Generador de consultas ofrece las siguientes ventajas:  
  
-   Trabajar visualmente o con comandos SQL.  
  
     El Generador de consultas incluye paneles gráficos que muestran la consulta visualmente y un panel de texto que muestra el texto SQL de la consulta. Puede trabajar en los paneles gráficos o de texto. El Generador de consultas sincroniza las vistas de forma que el texto de la consulta y la representación gráfica de la consulta coincidan siempre.  
  
-   Combinar tablas relacionadas.  
  
     Si agrega más de una tabla a la consulta, el Generador de consultas determinará automáticamente cómo están relacionadas las tablas y generará el comando de combinación correspondiente.  
  
-   Consultar o actualizar bases de datos.  
  
     Puede utilizar el Generador de consultas para devolver datos mediante instrucciones SELECT de Transact-SQL, o bien para crear consultas que actualicen, agreguen o eliminen registros de una base de datos.  
  
-   Ver y modificar los resultados inmediatamente.  
  
     Puede ejecutar la consulta y trabajar con un conjunto de registros en una cuadrícula que le permita desplazarse por los registros de la base de datos y modificarlos.  
  
 A pesar de que el Generador de consultas tiene limitaciones visuales para crear consultas SELECT, puede escribir el SQL para otros tipos de instrucciones, como las instrucciones DELETE y UPDATE, en el panel de texto. El panel gráfico se actualiza automáticamente para reflejar la instrucción SQL que escribió.  
  
 También puede proporcionar entradas directas escribiendo la consulta en el cuadro de diálogo de la tarea o del componente de flujo de datos, o bien en la ventana Propiedades.  
  
 Para más información, consulte [Query Builder](../../2014/integration-services/query-builder.md).  
  
## <a name="sql-in-files"></a>SQL en archivos  
 La instrucción SQL para la tarea Ejecutar SQL también puede residir en un archivo independiente. Por ejemplo, puede escribir una consulta utilizando herramientas como el Editor de consultas de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], guardarla en un archivo y después, leer la consulta del archivo al ejecutar un paquete. El archivo solo puede contener las instrucciones SQL que se van a ejecutar y comentarios. Para utilizar una instrucción SQL almacenada en un archivo, debe proporcionar una conexión de archivos que especifique el nombre y la ubicación del archivo. Para más información, consulte [File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="sql-in-variables"></a>SQL en variables  
 Si el origen de la instrucción SQL en la tarea Ejecutar SQL es una variable, debe proporcionar el nombre de la variable que contiene la consulta. La propiedad Value de la variable contiene el texto de la consulta. La propiedad ValueType de la variable se establece en un tipo de datos de cadena y luego se escribe o se copia la instrucción SQL en la propiedad Value. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) y [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md).  
  
  
