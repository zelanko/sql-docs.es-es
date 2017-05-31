---
title: "Asignación de tipos de datos para publicadores de Oracle | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: 6da0e4f4-f252-4b7e-ba60-d2e912aa278e
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6eb74ce4647046c91fa199c260abeb1ae1845f66
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="data-type-mapping-for-oracle-publishers"></a>Asignar tipos de datos para publicadores de Oracle
  Los tipos de datos de Oracle y de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no siempre coinciden de forma exacta. En la medida de lo posible, el tipo de datos coincidentes se selecciona automáticamente al publicar en una tabla Oracle. En los casos en que no queda clara una asignación de tipos de datos única, se proporcionan asignaciones alternativas de tipos de datos. Para obtener información acerca de cómo seleccionar asignaciones alternativas, vea la sección "Especificar asignaciones de tipos de datos alternativas" más adelante en este tema.  
  
 En la siguiente tabla se muestra cómo se asignan los tipos de datos de manera predeterminada entre Oracle y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando se mueven datos del publicador de Oracle al distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La columna Alternativas indica si existen asignaciones alternativas disponibles.  
  
|Tipo de datos de Oracle|Tipo de datos de SQL Server|Alternativas|  
|----------------------|--------------------------|------------------|  
|BFILE|VARBINARY(MAX)|Sí|  
|BLOB|VARBINARY(MAX)|Sí|  
|CHAR([1-2000])|CHAR([1-2000])|Sí|  
|CLOB|VARCHAR(MAX)|Sí|  
|DATE|DATETIME|Sí|  
|FLOAT|FLOAT|No|  
|FLOAT([1-53])|FLOAT([1-53])|No|  
|FLOAT([54-126])|FLOAT|No|  
|INT|NUMERIC(38)|Sí|  
|INTERVAL|DATETIME|Sí|  
|LONG|VARCHAR(MAX)|Sí|  
|LONG RAW|IMAGE|Sí|  
|NCHAR([1-1000])|NCHAR([1-1000])|No|  
|NCLOB|NVARCHAR(MAX)|Sí|  
|NUMBER|FLOAT|Sí|  
|NUMBER([1-38])|NUMERIC([1-38])|No|  
|NUMBER([0-38],[1-38])|NUMERIC([0-38],[1-38])|Sí|  
|NVARCHAR2([1-2000])|NVARCHAR([1-2000])|No|  
|RAW([1-2000])|VARBINARY([1-2000])|No|  
|REAL|FLOAT|No|  
|ROWID|CHAR(18)|No|  
|TIMESTAMP|DATETIME|Sí|  
|MARCA DE TIEMPO(0-7)|DATETIME|Sí|  
|TIMESTAMP(8-9)|DATETIME|Sí|  
|MARCA DE TIEMPO (0-7) CON ZONA HORARIA|VARCHAR(37)|Sí|  
|MARCA DE TIEMPO (8-9) CON ZONA HORARIA|VARCHAR(37)|No|  
|MARCA DE TIEMPO (0-7) CON ZONA HORARIA LOCAL|VARCHAR(37)|Sí|  
|MARCA DE TIEMPO (8-9) CON ZONA HORARIA LOCAL|VARCHAR(37)|No|  
|UROWID|CHAR(18)|No|  
|VARCHAR2([1-4000])|VARCHAR([1-4000])|Sí|  
  
## <a name="considerations-for-data-type-mapping"></a>Consideraciones para la asignación de tipos de datos  
 Tenga en cuenta los siguientes problemas de tipos de datos al replicar datos desde una base de datos de Oracle.  
  
### <a name="unsupported-data-types"></a>Tipos de datos no compatibles  
 Los siguientes tipos de datos no son compatibles; las columnas que tienen estos tipos de datos no se pueden replicar:  
  
-   Tipos de objetos  
  
-   Tipos XML  
  
-   Valores Varray  
  
-   Tablas anidadas  
  
-   Columnas que utilizan REF  
  
### <a name="the-date-data-type"></a>Tipo de datos DATE  
 Las fechas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] van del 1753 D.C. al 9999 D.C., mientras que las fechas del rango de Oracle van del 4712 A.C. al 4712 D.C. Si una columna de tipo FECHA contiene valores que están fuera del intervalo de SQL Server, seleccione el tipo de datos alternativo para la columna, que es VARCHAR(19).  
  
### <a name="float-and-number-types"></a>Tipos FLOAT y NUMBER  
 La escala y precisión especificadas durante la asignación de tipos de datos FLOAT y NUMBER depende de la escala y precisión especificadas para la columna mediante el tipo de datos de la base de datos de Oracle. La precisión es el número de dígitos de un número. La escala es el número de dígitos situados a la derecha de la coma decimal de un número. Por ejemplo, el número 123,45 tiene una precisión de 5 y una escala de 2.  
  
 Oracle permite que se definan números con una escala mayor que la precisión, como NUMBER(4,5), pero [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requiere que la precisión sea igual o mayor que la escala. Para garantizar que no hay truncamiento de datos, si la escala es mayor que la precisión en el publicador de Oracle, se define la precisión para que sea igual a la escala al asignar el tipo de datos: NUMBER(4,5) se asignaría como NUMERIC(5,5).  
  
> [!NOTE]  
>  Si no se especifica una escala y una precisión para NUMBER, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utiliza de forma predeterminada la escala (8) y precisión (38) máximas. Recomendamos definir una escala y precisión específicas en Oracle para mejorar el almacenamiento y el rendimiento al replicar los datos.  
  
### <a name="large-object-types"></a>Tipos de objetos grandes  
 Oracle admite hasta 4 gigabytes (GB), mientras que SQL Server admite hasta 2 GB. Los datos replicados por encima de 2 GB se truncan.  
  
 Si una tabla Oracle incluye una columna BFILE, los datos de la columna se almacenan en el sistema de archivos. La cuenta de usuario administrativo de la replicación debe tener acceso al directorio en el que se almacenan los datos, con la siguiente sintaxis:  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 Para obtener más información sobre los tipos de objetos grandes, vea la sección sobre consideraciones para los objetos grandes en el tema [Consideraciones y limitaciones de diseño de los publicadores de Oracle](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
## <a name="specifying-alternative-data-type-mappings"></a>Especificar asignaciones de tipos de datos alternativas  
 Normalmente, la asignación de tipos de datos predeterminada es adecuada, pero para muchos tipos de datos de Oracle puede seleccionar una asignación de tipos de datos entre un conjunto de asignaciones alternativas en lugar de utilizar la opción predeterminada. Hay dos formas de especificar asignaciones alternativas:  
  
-   Reemplazar la opción predeterminada artículo por artículo utilizando procedimientos almacenados o el Asistente para nueva publicación.  
  
-   Cambiar de forma global la opción predeterminada para todos los artículos futuros utilizando procedimientos almacenados (los valores predeterminados no se cambian para los artículos existentes).  
  
 Para especificar asignaciones de datos alternativas, vea [Specify Data Type Mappings for an Oracle Publisher](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md).  
  
## <a name="see-also"></a>Vea también  
 [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Consideraciones y limitaciones de diseño de los publicadores de Oracle](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
