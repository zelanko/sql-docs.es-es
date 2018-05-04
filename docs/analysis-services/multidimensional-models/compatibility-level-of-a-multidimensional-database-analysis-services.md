---
title: Nivel de compatibilidad de una base de datos Multidimensional (Analysis Services) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b25211d1eeacdbc09f4508aede2181c96a428e4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="compatibility-level-of-a-multidimensional-database-analysis-services"></a>Nivel de compatibilidad de una base de datos multidimensional (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], la propiedad de nivel de compatibilidad de la base de datos determina el nivel funcional de una base de datos. Los niveles de compatibilidad son únicos de cada tipo de modelo. Por ejemplo, un nivel de compatibilidad de **1100** tiene un significado diferente en función de si la base de datos es multidimensional o tabular.  
  
 En este tema se describe solo el nivel de compatibilidad para las bases de datos multidimensionales. Para obtener más información sobre las soluciones tabulares, vea [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).  
  
> [!NOTE]  
>  Los modelos tabulares tienen niveles de compatibilidad de la base de datos adicionales que no se pueden aplicar a los modelos multidimensionales. El nivel de compatibilidad **1103** no existe para los modelos multidimensionales. Vea [What is new for the Tabular model in SQL Server 2012 SP1 and compatibility level](http://go.microsoft.com/fwlink/?LinkId=301727) (Novedades del modelo tabular en SQL Server 2012 SP1 y nivel de compatibilidad) para obtener más información sobre **1103** para las soluciones tabulares.  
  
 **Niveles de compatibilidad para bases de datos multidimensionales**  
  
 Actualmente, el único comportamiento de la base de datos multidimensional que varía según el nivel funcional es la arquitectura de almacenamiento de cadenas. Al aumentar el nivel de compatibilidad de la base de datos, puede invalidar el límite máximo de 4 gigabytes para el almacenamiento de cadenas de medidas y dimensiones.  
  
 En el caso de una base de datos multidimensional, los valores válidos para la propiedad **CompatibilityLevel** incluyen los siguientes:  
  
|Configuración|Description|  
|-------------|-----------------|  
|**1050**|Este valor no es visible en el script ni en las herramientas pero corresponde a las bases de datos creadas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Cualquier base de datos que no tenga establecido explícitamente **CompatibilityLevel** se ejecuta de forma implícita en el nivel **1050** .|  
|**1100**|Es el valor predeterminado para las nuevas bases de datos creadas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. También puede especificarla si para las bases de datos creadas en versiones anteriores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se permite el uso de características que solo se admiten en este nivel de compatibilidad (a saber, mayor almacenamiento de cadenas para atributos de dimensión o medidas de recuento distintivas que contienen datos de cadena).<br /><br /> Las bases de datos que tienen la propiedad **CompatibilityLevel** establecida en **1100** obtienen una propiedad adicional, **StringStoresCompatibilityLevel**, que permite elegir un almacenamiento de cadenas alternativo para particiones y dimensiones.|  
  
> [!WARNING]  
>  Establecer la compatibilidad de la base de datos en un nivel superior es irreversible. Después de aumentar el nivel de compatibilidad a **1100**, debe seguir ejecutando la base de datos en servidores posteriores. No puede revertir al nivel **1050**. No puede adjuntar ni restaurar una base de datos **1100** en una versión de servidor anterior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="prerequisites"></a>Requisitos previos  
 Los niveles de compatibilidad de base de datos se presentaron en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Debe tener [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o posterior para ver o establecer el nivel de compatibilidad de la base de datos.  
  
 La base de datos no puede ser un cubo local. Los cubos locales no admiten la propiedad **CompatibilityLevel** .  
  
 La base de datos se debe haber creado en una versión anterior (SQL Server 2008 R2 o versiones anteriores) y después adjuntarse o restaurarse en un servidor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o posterior. Las bases de datos implementadas en SQL Server 2012 ya están en el nivel **1100** y no se pueden cambiar para que se ejecuten en un nivel inferior.  
  
## <a name="determine-the-existing-database-compatibility-level-for-a-multidimensional-database"></a>Determinar el nivel de compatibilidad de la base de datos existente para una base de datos multidimensional  
 La única forma de ver o modificar el nivel de compatibilidad de la base de datos es mediante XMLA. Puede ver o modificar el script XMLA que especifica la base de datos en SQL Server Management Studio.  
  
 Si busca la definición de XMLA de una base de datos para la propiedad **CompatibilityLevel** y no existe, lo más probable es que tenga una base de datos en el nivel **1050** .  
  
 En la sección siguiente se ofrecen instrucciones para ver y modificar el script XMLA.  
  
## <a name="set-the-database-compatibility-level-in-sql-server-management-studio"></a>Establecer el nivel de compatibilidad de la base de datos en SQL Server Management Studio  
  
1.  Antes de aumentar el nivel de compatibilidad, haga copia de seguridad de la base de datos por si desea revertir los cambios posteriormente.  
  
2.  Con SQL Server Management Studio, conéctese al servidor de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospede la base de datos.  
  
3.  Haga clic con el botón derecho en el nombre de la base de datos, seleccione **Incluir la base de datos como**, seleccione **ALTER To**y, después, seleccione **Nueva ventana del Editor de consultas**. Una representación XMLA de la base de datos se abrirá en una nueva ventana.  
  
4.  Copie el elemento XML siguiente:  
  
    ```  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    ```  
  
5.  Péguelo después del elemento de cierre `</Annotations>` y antes del elemento `<Language>` . El XML debería presentar una apariencia similar a la del ejemplo siguiente:  
  
    ```  
    </Annotations>  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    <Language>1033</Language>  
    ```  
  
6.  Guarde el archivo.  
  
7.  Para ejecutar el script, haga clic en **Ejecutar** en el menú Consulta o presione F5.  
  
## <a name="supported-operations-that-require-the-same-compatibility-level"></a>Operaciones admitidas que requieren el mismo nivel de compatibilidad  
 Las siguientes operaciones requieren que las bases de datos de origen compartan el mismo nivel de compatibilidad.  
  
1.  Solo se admite la combinación de particiones de bases de datos distintas si ambas bases de datos comparten el mismo nivel de compatibilidad.  
  
2.  El uso de dimensiones vinculadas desde otra base de datos requiere el mismo nivel de compatibilidad. Por ejemplo, si desea usar una dimensión vinculada de una base de datos de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] en una de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , debe pasar la base de datos de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] a un servidor de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y establecer el nivel de compatibilidad en **1100**.  
  
3.  La sincronización de servidores solo se admite para los servidores que comparten la misma versión y nivel de compatibilidad de la base de datos.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Después de aumentar el nivel de compatibilidad de la base de datos, puede establecer la propiedad **StringStoresCompatibilityLevel** en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Esto aumenta el almacenamiento de cadenas para medidas y dimensiones. Para obtener más información sobre esta característica, vea [Configurar el almacenamiento de cadenas para dimensiones y particiones](../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md).  
  
## <a name="see-also"></a>Vea también  
 [Restaurar, sincronizar y realizar copias de seguridad de bases de datos &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
