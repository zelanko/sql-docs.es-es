---
title: Conjunto de filas DISCOVER_CSDL_METADATA | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: a2d3cffd-a2c4-411c-b244-9e41ebe30939
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7221a67fb73c55b0173da2c10826d75003c50e6d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="discovercsdlmetadata-rowset"></a>DISCOVER_CSDL_METADATA, conjunto de filas
  Devuelve información sobre un modelo de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] (ya sea tabular o multidimensional), proporcionando la definición del modelo en el formato CSDLBI (lenguaje de definición de esquemas conceptuales con anotaciones BI). CSDLBI está basado en CSDL, un esquema XML utilizado por Entity Data Framework para la comunicación entre un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y el cliente de [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] . Las anotaciones Business Intelligence (BI) proporcionan metadatos adicionales sobre los modelos tabulares y los objetos incluidos en ellos. Para más información sobre los modelos de datos tabulares, vea [Anotaciones de CSDL para Business Intelligence &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md).  
  
 El contexto de seguridad del comando afecta al conjunto de filas que se devuelve. Se requiere que los permisos Read en la instancia de Analysis Services obtengan la definición de CSDL desde servidor.  
  
 El identificador de idioma del cliente que emite la solicitud del conjunto de filas se incluye en la cadena de conexión para el comando, y afecta al idioma que se muestra en varias propiedades que se devuelven como parte del conjunto de filas.  Para obtener información acerca de las propiedades y la descripción que pueden verse afectadas por el identificador de idioma, vea la sección Comentarios.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_CSDL_METADATA** contiene las siguientes columnas.  
  
|**Nombre de columna**|**Indicador de tipo**|**Restricción**|**Description**|  
|---------------------|------------------------|---------------------|---------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Sí|Especifica el nombre de la base de datos cuya descripción CSDLBI se solicita. Si se omite, se utiliza la base de datos actual.<br /><br /> Esta restricción es obligatoria para todos los tipos de modelos.|  
|**PERSPECTIVE_ID**|**DBTYPE_WSTR**|Sí|Especifica el identificador de una perspectiva que se ha definido en el modelo especificado por CATALOG_NAME.<br /><br /> Es una restricción opcional. Se aplica a todos los tipos de modelos.|  
|**PERSPECTIVE_NAME**|**DBTYPE_WSTR**|Sí|Especifica el nombre de una perspectiva que se ha definido en el modelo especificado por CATALOG_NAME.<br /><br /> Esta restricción es obligatoria cuando el modelo tabular incluye perspectivas o cuando una solución multidimensional incluye varios cubos o varias perspectivas.|  
|**METADATOS**|**DBTYPE_WSTR**|No|Cadena que contiene la definición XML de un origen de datos y sus propiedades, de acuerdo con el esquema CSDLBI.|  
|**CUBE_ID**|**DBTYPE_WSTR**|Sí|Identificador de cadena.<br /><br /> Esta restricción es opcional para las bases de datos multidimensionales. Si hay varios cubos disponibles y se omite la restricción, se devuelve el cubo predeterminado.|  
  
## <a name="remarks"></a>Comentarios  
 DISCOVER_CSDL_METADATA tiene los requisitos siguientes:  
  
-   La solicitud DISCOVER producirá un error si no se especifica una base de datos mediante la restricción CATALOG_NAME.  
  
-   En un modelo tabular con varias perspectivas, se requiere un identificador de perspectiva.  
  
-   En los modelos multidimensionales, se requiere tanto el nombre del catálogo como el nombre del cubo (perspectiva).  
  
-   Si una perspectiva se proporciona como una restricción, se devuelve el mismo conjunto de filas de CSDL que se devolvió para el modelo. Sin embargo, los objetos que estén presentes en el modelo pero que no se incluyan en la perspectiva especificada se marcan como **Hidden** = TRUE.  
  
-   Para las tablas y columnas, la solicitud DISCOVER siempre devuelve un valor del cubo. Si no está establecida la propiedad de dimensión del cubo, la solicitud devuelve el valor de la dimensión.  
  
-   La solicitud DISCOVER no puede devolver ninguna medida ni columna calculada que contenga un error semántico.  
  
-   La solicitud DISCOVER no devolverá ninguna información para los objetos que no tienen valores de propiedad. La solicitud DISCOVER tampoco devolverá los valores para los atributos que utilizan el valor predeterminado.  
  
 La cadena XML que se devuelve en el conjunto de filas puede incluir las propiedades o los valores específicos del idioma siguientes. Por ejemplo, si se emite la solicitud de conjunto de filas desde un cliente con el LCID 0403 (catalán de España), la propiedad devolverá los valores siguientes correspondientes para dicho idioma. Si las traducciones no están disponibles en el servidor, se devuelve la cadena para el idioma predeterminado del servidor.  
  
-   Caption  
  
-   Calificador  
  
-   SortDirection  
  
-   IsRightToLeft  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 La consulta XMLA siguiente devuelve la representación CSDL del ejemplo de modelo tabular AdventureWorks 2012. Cada solución tabular solo puede contener un modelo, por lo que la restricción PERSPECTIVE_NAME se puede dejar en blanco. Sin embargo, este modelo contiene varias perspectivas.  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>AdventureWorks2012Tabular</CATALOG_NAME>  
                <PERSPECTIVE_NAME>EMPLOYEE</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
</Discover>  
  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 La consulta XMLA siguiente devuelve las representaciones CSDLBI de cubo de operaciones de Contoso. Es necesaria la restricción VERSION para consultar una base de datos multidimensional. La base de datos de Contoso Retail contiene dos cubos, de modo que se hace referencia al cubo de operaciones mediante restricciones PERSPECTIVE_NAME.  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>Contoso_Retail</CATALOG_NAME>  
                <PERSPECTIVE_NAME>Operation</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
 </Discover>  
  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|3444B255-171E-4cb9-AD98-19E57888A75F|  
|ADOMDNAME|Csdl|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Anotaciones de CSDL para Business Intelligence &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
  
