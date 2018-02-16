---
title: "Crear una dimensión mediante el uso de una tabla existente | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchies [Analysis Services], dimensions
- main dimension tables
- dimensions [Analysis Services], standard
- standard dimensions [Analysis Services]
ms.assetid: edd96fbe-1b1c-445a-95d6-7a025e0ee868
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b748f139d4eed14ea9d00d275aedcc8ef8fc9fec
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="create-a-dimension-by-using-an-existing-table"></a>Crear una dimensión usando una tabla existente
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede usar el Asistente para dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para crear una dimensión a partir de una tabla existente. Para hacerlo, debe seleccionar la opción **Usar una tabla existente** en la página **Seleccionar método de creación** del asistente. Con esta opción, el asistente basa la estructura de la dimensión en las tablas de dimensiones, sus columnas y las posibles relaciones entre esas columnas en una vista del origen de datos existente. El asistente prueba los datos en la tabla de origen y las tablas relacionadas. Usa estos datos para definir columnas de atributos que se basan en las columnas de las tablas de dimensiones, así como para definir jerarquías de atributos (denominadas jerarquías *definidas por el usuario* ). Tras utilizar el Asistente para dimensiones para crear su dimensión, puede usar el Diseñador de dimensiones para agregar, quitar o configurar atributos y jerarquías de la dimensión.  
  
 Si está utilizando una tabla existente para crear una dimensión, el Asistente para dimensiones lo guía a través de los siguientes pasos:  
  
-   Especificar la información de origen  
  
-   Seleccionar tablas relacionadas  
  
-   Seleccionar atributos de dimensión  
  
-   Definir la inteligencia de cuentas  
  
> [!NOTE]  
>  Para consultar las instrucciones paso a paso que corresponden a la información presentada en este tema, vea [Crear una dimensión usando el Asistente para dimensiones](../../analysis-services/multidimensional-models/create-a-dimension-using-the-dimension-wizard.md).  
  
## <a name="specifying-the-source-information"></a>Especificar la información de origen  
 La información de origen se especifica en la página **Especificar información de origen** . Este proceso se empieza seleccionando la vista del origen de datos que contiene la tabla en la que desea basar la dimensión. A continuación, debe definir la tabla de dimensiones principal de la dimensión que va a definir. La tabla de dimensiones principal es la que está vinculada directamente a la tabla de hechos. Por ejemplo, especifique una tabla Product como tabla principal para una dimensión Products o una tabla Employee para una dimensión Employees. El asistente selecciona automáticamente una columna de clave que está basada en la clave principal en la vista del origen de datos. Sin embargo, puede cambiar según corresponda la columna de clave. La columna de clave determina los miembros de dimensión. Por ejemplo, tendría que definir ProductKey como columna de clave de una dimensión Product.  
  
 Si lo desea, puede definir una columna que contenga el nombre de miembro. De manera predeterminada, el nombre de miembro que se mostrará a los usuarios será el valor de la columna de clave. Los valores de una columna de clave (como por ejemplo ProductID o EmployeeID) son a menudo claves únicas, generadas por el sistema, sin significado para el usuario. A menudo, puede proporcionar al usuario información más significativa cambiando el nombre que se ve por un valor correspondiente de alguna otra columna de la dimensión. Por ejemplo, puede definir una columna de nombre de miembro que contenga nombres de productos o de empleados. Si cambia el nombre de miembro, los usuarios ven un nombre más descriptivo, pero las consultas siguen utilizando los valores de columna de clave para distinguir correctamente los miembros que comparten el mismo nombre. Si especifica una clave compuesta para la columna de clave, debe especificar también la columna que proporcione los valores de miembro al atributo clave. Para más información sobre cómo configurar las propiedades de los atributos, vea [Referencia de las propiedades de los atributos de dimensión](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
## <a name="selecting-related-tables"></a>Seleccionar tablas relacionadas  
  
> [!NOTE]  
>  El asistente se salta este paso si la tabla de dimensiones principal no tiene relaciones definidas con otras tablas de dimensiones en la vista del origen de datos.  
  
 Si está generando una dimensión de copo de nieve, debe especificar las tablas relacionadas a partir de las cuales se definirán atributos adicionales en la página **Seleccionar tablas relacionadas** . Por ejemplo, está generando una dimensión de cliente en la que desea definir una tabla geográfica de clientes. En este caso, podría definir una tabla geográfica como una tabla relacionada.  
  
## <a name="selecting-dimension-attributes"></a>Seleccionar atributos de dimensión  
 Una vez seleccionadas las tablas de dimensiones, debe usar la página **Seleccionar los atributos de la dimensión** para seleccionar los atributos que quiera incluir en la dimensión desde esas tablas. Todas las columnas subyacentes de todas estas tablas están disponibles como posibles atributos de dimensión. El atributo de clave de dimensión debe estar seleccionado y habilitado para ser examinado.  
  
 De forma predeterminada, el asistente establece el tipo de un atributo en **Regular**. Sin embargo, es posible que usted quiera asignar atributos concretos a un tipo de atributo diferente que represente mejor los datos. Por ejemplo, la tabla dbo.DimAccount de la base de datos de ejemplo [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW contiene una columna AccountCodeAlternateKey que proporciona el número de cuenta. En lugar de establecer el tipo en **Regular** para este atributo, podría desear asignar el atributo al tipo **Account Number** .  
  
> [!NOTE]  
>  Si el tipo de dimensión y los tipos de atributo estándar no están establecidos al crear la dimensión, use el Asistente de Business Intelligence para establecerlos una vez creada la dimensión. Para más información, vea [Agregar inteligencia de dimensiones a una dimensión](../../analysis-services/multidimensional-models/bi-wizard-add-dimension-intelligence-to-a-dimension.md) o (para una dimensión de tipo Accounts) [Agregar inteligencia de cuentas a una dimensión](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
 El asistente establece automáticamente el tipo de dimensión basándose en los tipos de atributo especificados. Los tipos de atributo especificados en el asistente determinan la propiedad **Type** de los atributos. El valor de la propiedad **Type** de la dimensión y sus atributos proporcionan información acerca del contenido de una dimensión al servidor y a las aplicaciones cliente. En algunos casos, el valor de la propiedad **Type** solo constituye una guía para las aplicaciones cliente y es opcional. En otros casos, como en las dimensiones Accounts, Time o Currency, el valor de la propiedad **Type** determina comportamientos específicos basados en el servidor y puede que sea necesario implementar ciertos comportamientos del cubo.  
  
 Para más información sobre tipos de atributos y dimensiones, vea [Tipos de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)y [Configurar tipos de atributos](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md).  
  
## <a name="defining-account-intelligence"></a>Definir la inteligencia de cuentas  
  
> [!NOTE]  
>  El Asistente para dimensiones solo muestra este paso si se ha definido un atributo de dimensión **Tipo de cuenta** en la página **Seleccionar los atributos de la dimensión** del asistente.  
  
 En la página **Definir la inteligencia de cuentas** puede crear una dimensión de tipo de cuenta. Si va a crear una dimensión de tipo de cuenta, debe asignar tipos de cuenta estándar admitidos por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a miembros del atributo de tipo de cuenta de la dimensión. El servidor utiliza estas asignaciones para proporcionar alias y funciones de agregación independientes para cada tipo de datos de cuenta.  
  
 Para asignar estos tipos de cuenta, el asistente proporciona las columnas siguientes a una tabla:  
  
-   La columna **Tipos de cuenta de tabla de origen** muestra los tipos de cuenta de la tabla de origen de datos.  
  
-   La columna **Tipos de cuenta integrados** muestra los tipos de cuenta estándar correspondientes compatibles con el servidor. Si los datos de origen usan nombres estándar, el asistente asigna automáticamente el tipo de origen al tipo de servidor y rellena la columna **Tipos de cuenta integrados** con esta información. Si el servidor no asigna los tipos de cuenta o si usted quiere cambiar la asignación, seleccione un tipo diferente en la lista de la columna **Tipos de cuenta integrados** .  
  
> [!NOTE]  
>  Si los tipos de cuenta no se asignan cuando el asistente crea una dimensión Accounts, use el Asistente de Business Intelligence para configurar las asignaciones una vez creada la dimensión. Para más información, vea [Agregar inteligencia de cuentas a una dimensión](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="completing-the-wizard"></a>Finalizar el Asistente  
 El asistente examina las tablas de dimensiones para detectar las relaciones. El asistente creará automáticamente las relaciones de atributo entre los atributos clave de dimensiones de copo de nieve.  
  
 El asistente detecta también automáticamente si en la dimensión existe una relación de elementos primarios y secundarios. Una relación primario-secundario existe cuando un atributo primario hace referencia a miembros del atributo clave de la dimensión. Esta relación define relaciones jerárquicas y rutas de agregación entre miembros hoja de la dimensión. Para más información sobre las jerarquías de elementos primarios y secundarios, vea [Atributos en las jerarquías de elementos primarios y secundarios](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
 Para terminar el asistente, en la página **Finalización del asistente** , escriba un nombre para la nueva dimensión y revise la estructura de la dimensión.  
  
## <a name="see-also"></a>Vea también  
 [Crear una dimensión generando una tabla no sea de tiempos en el origen de datos](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)   
 [Crear una dimensión de tiempo generando una tabla de tiempos](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Referencia de propiedades de atributos de dimensión](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [Crear una dimensión de tiempo generando una tabla de tiempos](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Crear una dimensión generando una tabla no sea de tiempos en el origen de datos](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
