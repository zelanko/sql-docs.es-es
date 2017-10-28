---
title: Convertir objetos de base de datos de Access (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases
- Access databases, converting schemas
- conversion
- conversion, converting schemas
- indexes, altering
- metadata
- metadata, altering
- metadata, converting
- migrating databases, one-click
- one-click migration
- schemas
- schemas, converting
- SQL
- SQL, converting
- syntax
- syntax, converting
- tables, altering
- translating Access to SQL Azure
- translating Access to SQL Server
ms.assetid: e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5fd1535f35afdfa53895816da2e3e32f539c04b5
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="converting-access-database-objects-accesstosql"></a>Convertir objetos de base de datos de Access (AccessToSQL)
Después de haber agregado las bases de datos de Access y conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, SSMA muestra los metadatos para el acceso y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de base de datos de SQL Azure. Puede seleccionar ahora los objetos de base de datos de Access y, a continuación, convertir los esquemas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquemas de SQL Azure.  
  
## <a name="the-conversion-process"></a>El proceso de conversión  
Convertir objetos de base de datos toma las definiciones de objeto de los metadatos de acceso, se convierte en equivalente [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxis y, a continuación, se carga esta información en el proyecto. A continuación, puede ver el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de SQL Azure y sus propiedades mediante el uso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o en el Explorador de metadatos de SQL Azure.  
  
> [!IMPORTANT]  
> Convertir objetos no crea los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Solo convierte las definiciones de objeto y almacena la información en el proyecto SSMA.  
  
Durante la conversión, SSMA imprime el estado para el panel de resultados, error, advertencia y mensajes informativos en el panel de lista de errores. Utilice esta información para determinar si tiene que modificar las bases de datos de acceso o el proceso de conversión para obtener los resultados de la conversión deseada. También puede utilizar la información de la [preparar bases de datos de Access para la migración](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114) tema para determinar qué se y no se convertirán.  
  
## <a name="setting-conversion-options"></a>Establecer las opciones de conversión  
Antes de convertir objetos, revise las opciones de conversión de proyecto en el **configuración del proyecto** cuadro de diálogo. Mediante este cuadro de diálogo, puede establecer cómo SSMA convierte las columnas indizadas memorando, claves principales, las restricciones foreign key, las marcas de tiempo y tablas sin índices. Para obtener más información, vea [configuración del proyecto (conversión)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>Resultados de la conversión  
La siguiente tabla muestra qué objetos de acceso se convierten y resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de SQL Azure:  
  
|Objeto de acceso|Objeto resultante de SQL Server|  
|-----------------|-------------------------------|  
|table|table|  
|column|column|  
|índice|índice|  
|clave externa|clave externa|  
|Query|ver<br /><br />Consultas más SELECT se convierten en vistas. Otras consultas, como las consultas de actualización, no se migran.<br /><br />Consultas SELECT que toman parámetros no se convierten, ni tampoco las consultas de tablas de referencias cruzadas.|  
|informe|no se pudo convertir|  
|formulario|no se pudo convertir|  
|(Macro)|no se pudo convertir|  
|Módulo|no se pudo convertir|  
|Valor predeterminado|Valor predeterminado|  
|Permitir cero propiedad de columna de longitud|restricción CHECK|  
|regla de validación de la columna|restricción CHECK|  
|regla de validación de tabla|restricción CHECK|  
|clave principal|clave principal|  
  
## <a name="converting-access-objects"></a>Convertir objetos de acceso  
Para convertir objetos de base de datos de Access, primero debe seleccionar los objetos que desea convertir y, a continuación, tener SSMA para realizar la conversión. Para ver los mensajes de salida durante la conversión, en la **vista** menú, seleccione **salida**.  
  
**Para seleccionar y convierte los objetos de base de datos de Access a la sintaxis de SQL Server o SQL Azure**  
  
1.  En el Explorador de metadatos de acceso, expanda **acceso metabase**y, a continuación, expanda **bases de datos**.  
  
2.  Realice uno o varios de los procedimientos siguientes:  
  
    -   Para convertir todas las bases de datos, active la casilla situada junto a **bases de datos**.  
  
    -   Para convertir u omitir las bases de datos individuales, active o desactive la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para convertir u omitir las consultas, expanda la base de datos y, a continuación, active o desactive el **consultas** casilla de verificación.  
  
    -   Para convertir u omitir las tablas individuales, expanda la base de datos, **tablas**y, a continuación, active o desactive la casilla situada junto a la tabla.  
  
3.  Realice una de las siguientes operaciones:  
  
    -   Para convertir esquemas, haga clic en **bases de datos** y seleccione **convertir esquema**.  
  
        También puede convertir los objetos individuales. Para convertir un objeto, con independencia de qué objetos están seleccionados, haga clic en el objeto y seleccione **convertir esquema**.  
  
        Cuando se ha convertido un objeto, lo aparece en negrita en el Explorador de metadatos de acceso.  
  
    -   Para convertir, cargar y migrar esquemas y datos en un solo paso, haga clic en las bases de datos y seleccione **convertir, cargar y migrar**.  
  
4.  Revise los mensajes de la **salida** panel y los errores y advertencias en el **lista de errores** panel.  
  
## <a name="altering-tables-and-indexes"></a>Modificar tablas e índices  
Después de convertir los metadatos de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o metadatos de SQL Azure, y antes de cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, puede modificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tablas de SQL Azure y los índices.  
  
**Para modificar las propiedades de tabla o índice**  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure, seleccione la tabla o índice que desea modificar.  
  
2.  En el **tabla** , haga clic en la propiedad que desea modificar y, a continuación, escriba o seleccione la nueva configuración. Por ejemplo, puede cambiar nvarchar (15) a nvarchar (20), o seleccionar una casilla de verificación para hacer que una columna de tabla que aceptan valores NULL.  
  
    Mueva el cursor fuera de la celda de la propiedad que ha cambiado. Puede hacerlo haciendo clic en otra fila o al presionar la tecla Tab.  
  
3.  Haga clic en **Aplicar**.  
  
Ahora puede ver los cambios en el código en el **SQL** ficha.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [cargará los objetos de base de datos convertida en SQL Server](http://msdn.microsoft.com/en-us/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

