---
title: Importar datos (SSAS Tabular) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6617b2a2-9f69-433e-89e0-4c5dc92982cf
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fc8728c2a4e023fb03e0e2de8e3c457e0f15fd72
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204053"
---
# <a name="import-data-ssas-tabular"></a>Importar datos (SSAS tabular)
  Puede importar datos en un modelo tabular desde una gran variedad de orígenes. En los temas de esta sección se describe cómo utilizar el Asistente para la importación de tablas para conectarse y seleccionar los datos que se van a importar en un proyecto de modelos.  
  
> [!IMPORTANT]  
>  Si alguna de las tablas del modelo contiene un gran número de filas, considere importar únicamente un subconjunto de los datos durante la creación del modelo. Si importa un subconjunto de los datos, puede reducir el tiempo de procesamiento y el consumo de recursos de servidor de bases de datos del área de trabajo.  
  
 Con el Asistente para la importación de tablas, puede importar datos desde los orígenes de datos siguientes:  
  
|**Origen de datos**|**Descripción**|  
|---------------------|---------------------|  
|**Bases de datos relacionales**|Los orígenes de datos relacionales incluyen:<br /><br /> Microsoft SQL Server<br /><br /> Microsoft SQL Azure<br /><br /> Almacenamiento de datos paralelo de Microsoft SQL Server<br /><br /> Microsoft Access<br /><br /> Oracle<br /><br /> Teradata<br /><br /> Sybase<br /><br /> Informix<br /><br /> IBM DB2<br /><br /> OLEDB/ODBC|  
|**Orígenes multidimensionales**|Cubo de Microsoft SQL Server Analysis Services|  
|**Fuentes de datos**|Las fuentes de distribución de datos incluyen:<br /><br /> Informe de Microsoft Reporting Services<br /><br /> Conjunto de datos de Azure DataMarket<br /><br /> Fuentes Atom desde un proveedor público o corporativo|  
|**Archivos de texto**|Los archivos de texto incluyen:<br /><br /> Archivos de Excel (.xlsx)<br /><br /> Archivo de texto (.txt)|  
  
 Además de importar datos usando el Asistente para la importación de tablas, también puede pegar datos copiados (desde el Portapapeles) en una tabla. Los datos pegados se comportan de forma diferente a los datos que se han importado desde otros orígenes de datos. Los datos pegados en tablas no tienen la propiedad Nombre de conexión o Datos de origen. Los datos pegados se guardan en el archivo Model.bim. Los datos pegados se guardan junto con el proyecto o el archivo Model.bim.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Importar datos de un origen de datos relacionales &#40;SSAS Tabular&#41;](import-from-a-relational-data-source-ssas-tabular.md)|Describe cómo importar datos de orígenes de datos relacionales, como las bases de datos de Microsoft SQL Server, Oracle o Teradata.|  
|[Importar datos de un origen de datos multidimensionales &#40;SSAS Tabular&#41;](import-from-a-multidimensional-data-source-ssas-tabular.md)|Describe cómo importar datos de un cubo multidimensional de SQL Server Analysis Services.|  
|[Importar desde una fuente de datos &#40;SSAS Tabular&#41;](import-from-a-data-feed-ssas-tabular.md)|Describe cómo importar datos desde una fuente de distribución de datos, como un informe de Microsoft Reporting Services o un conjunto de datos de Azure DataMarket.|  
|[Importar desde un archivo de texto &#40;SSAS Tabular&#41;](import-from-a-text-file-ssas-tabular.md)|Describe cómo importar datos desde un libro de Microsoft Excel o un archivo de texto.|  
|[Copiar y pegar datos &#40;SSAS Tabular&#41;](copy-and-paste-data-ssas-tabular.md)|Describe cómo agregar datos a una tabla existente en el Diseñador de modelos usando Pegar, y Pegar y anexar.|  
  
  