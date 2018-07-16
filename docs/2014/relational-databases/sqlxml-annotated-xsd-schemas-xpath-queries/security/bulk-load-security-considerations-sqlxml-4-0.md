---
title: Consideraciones de seguridad de carga (SQLXML 4.0) de forma masiva | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, XML Bulk Load
- bulk load [SQLXML], security
- security [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], security
ms.assetid: 192fc6d4-ecbc-4a4d-a5cb-55e1f64af318
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 428041edc6418e71f08b757b622b6e5ebb640dba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280561"
---
# <a name="bulk-load-security-considerations-sqlxml-40"></a>Consideraciones de seguridad sobre la carga masiva (SQLXML 4.0)
  A continuación se muestran una serie de instrucciones de seguridad para utilizar la carga masiva XML:  
  
-   Cuando especifique que la operación de carga masiva debe realizarse como una transacción, debe utilizar la propiedad `TempFilePath` para especificar una carpeta en la que crear los archivos temporales.  
  
     El proceso de carga masiva crea estos archivos temporales con los siguientes permisos:  
  
    -   Se concede acceso de lectura/escritura/eliminación al proceso de carga masiva.  
  
    -   Se concede permiso de lectura a todos los usuarios porque se desconoce la cuenta con la que Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] obtendrá acceso a estos archivos. Puede restringir el acceso a estos archivos temporales estableciendo los permisos adecuados en la carpeta que los contiene.  
  
-   La carga masiva XML propiamente dicha no tiene ninguna configuración de permisos. Se asume que la base de datos está configurada correctamente y que el contexto del usuario (es decir, el inicio de sesión de la carga masiva) tiene establecidos los permisos adecuados.  
  
-   En el modo no transaccional, si se produce un error durante el proceso de carga masiva, los datos pueden quedar en un estado parcialmente cargado. La carga masiva simplemente se detendrá en el punto donde esto ocurra. El modo transaccional puede utilizarse para mitigar este problema.  
  
-   Cuando se producen errores de carga masiva, éstos pueden incluir información sobre la base de datos. Por ejemplo, pueden incluir el nombre de una tabla o columna o información del tipo de columna. Cuando utilice la carga masiva, debe tener cuidado de detectar los errores que se produzcan durante el proceso de carga masiva y devolver un mensaje de error genérico, en lugar de exponer los errores directamente a los usuarios.  
  
-   La carga masiva no establece ningún límite en la cantidad de datos con los que puede trabajar. La carga masiva no realiza ninguna comprobación de tamaño de los datos que va a cargarse. Es responsabilidad del usuario que ejecuta la carga masiva asegurarse de que hay suficiente memoria como para procesar el archivo especificado y suficiente espacio en la base de datos como para almacenar los datos que están cargándose.  
  
-   La carga masiva no intenta usar los datos suministrados como código. Los datos de entrada no se ejecutan nunca de ninguna forma. Todo el código o los comando de los datos de entrada se consideran datos normales y no se ejecutan.  
  
-   La carga masiva puede realizar cambios de formato en los datos proporcionados basándose en las diferencias entre los modelos de datos XML y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por ejemplo, el formato para especificar una hora es distinto. La carga masiva intentará resolver estas diferencias. Como resultado, es posible que se pierdan algunos datos de precisión.  
  
-   La carga masiva no establece ningún límite en la cantidad de tiempo que tarda en procesar los datos. El procesamiento continúa hasta que se completa o hasta que se produce un error.  
  
-   La carga masiva es capaz de crear y eliminar tablas temporales en la base de datos y necesita permisos para hacerlo. Se concederán permisos sobre estas tablas al mismo usuario que esté conectándose a la base de datos para el proceso de carga masiva.  
  
-   La carga masiva puede crear y eliminar los archivos temporales utilizados durante el procesamiento en modo transaccional y necesita permisos para hacerlo. Estos archivos se crean con los mismos permisos que el usuario actual del subproceso dentro del que se ejecuta la carga masiva.  
  
-   Si el usuario establece un archivo de registro de errores para que SQLXML escriba errores en él, cada vez se ejecute la carga masiva, el archivo se sobrescribirá con los datos del último proceso de carga masiva.  
  
## <a name="see-also"></a>Vea también  
 [Realizar la carga masiva de datos XML &#40;SQLXML 4.0&#41;](../bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
  
  
