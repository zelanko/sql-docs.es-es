---
title: Descripción de la generación incremental | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- incremental generation [Analysis Services]
- Schema Generation Wizard, incremental generation
- relational schema [Analysis Services], incremental generation
ms.assetid: 3ca0aa63-3eb5-4fe9-934f-8e96dee84eaa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ace9bbbbbc023d14dbce91a176f7d05ad19d699b
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811061"
---
# <a name="understanding-incremental-generation"></a>Descripción de la generación incremental
  Tras la generación del esquema inicial, es posible cambiar las definiciones de cubo y de dimensión mediante [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y volver a ejecutar el Asistente para generar esquemas. El asistente actualiza el esquema de la base de datos del área de asunto y de la vista de origen de datos asociada para reflejar los cambios y conservar los datos que existen actualmente en las tablas que se van a volver a generar, en la medida de lo posible. Si las tablas han cambiado tras la generación inicial, el Asistente para generar esquemas conservará en la medida de lo posible los cambios siguiendo estas reglas:  
  
-   Si la tabla se generó anteriormente utilizando el asistente, entonces se sobrescribirá. Para evitar que se sobrescriba una tabla generada con el asistente, debe cambiarse la propiedad `AllowChangesDuringGeneration` de la tabla en la vista de origen de datos a `false`. Al asumir el control de una tabla, ésta recibe el mismo tratamiento que una tabla definida por el usuario y no se ve afectada por la regeneración. Tras quitar una tabla de la generación, puede cambiarse más adelante la propiedad `AllowChangesDuringGeneration` de la tabla en la vista de origen de datos a `true` y volver a abrir la tabla para que tengan efecto los cambios realizados por el asistente. Para obtener más información, vea [Cambiar las propiedades de una vista del origen de datos &#40;Analysis Services&#41;](change-properties-in-a-data-source-view-analysis-services.md).  
  
-   Si se ha agregado una tabla a la vista de origen de datos o a la base de datos subyacente por un medio distinto del asistente, no se sobrescribe la tabla.  
  
 Si el Asistente para generar esquemas vuelve a generar tablas que se generaron anteriormente en la base de datos del área de asunto, puede elegir que el asistente conserve los datos existentes en las tablas.  
  
## <a name="supporting-data-preservation"></a>Admitir conservación de datos  
 Como regla general, el Asistente para generar esquemas conserva los datos almacenados en las tablas que generó. Además, si se agregan columnas a las tablas generadas por el asistente, el asistente conserva también los datos. Puede utilizarse esta función para agregar o modificar las dimensiones y cubos y a continuación volver a generar los objetos subyacentes sin tener que volver a cargar los datos almacenados en las tablas subyacentes.  
  
> [!NOTE]  
>  Si carga datos desde archivos de texto delimitado, también podrá elegir si desea que el Asistente para generar esquemas sobrescriba los archivos y datos que contienen durante la regeneración. Los archivos de texto pueden sobrescribirse completamente o no sobrescribirse. El Asistente para generar esquemas no sobrescribe parcialmente los archivos. De manera predeterminada, no se sobrescriben los archivos.  
  
### <a name="partial-preservation"></a>Conservación parcial  
 El Asistente para generar esquemas no puede conservar los datos existentes en algunos casos. En la siguiente tabla se muestran ejemplos de situaciones en las que el asistente no puede conservar todos los datos existentes en las tablas subyacentes durante la regeneración.  
  
|Cambio de tipo de datos|Tratamiento|  
|-------------------------|---------------|  
|Cambio de tipo de datos incompatible|El Asistente para generar esquemas utiliza, en la medida de lo posible, conversiones de tipos de datos estándar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para convertir los datos de un tipo de datos existente a otro. Sin embargo, al cambiar el tipo de datos de un atributo a otro tipo incompatible con los datos existentes, el asistente quita los datos de la columna afectada.|  
|Errores de integridad referencial|Si se cambia una dimensión o un cubo que contiene datos y el cambio provoca un error de integridad referencial durante la regeneración, el Asistente para generar esquemas quita todos los datos de la tabla de clave externa. No solo se quitan los datos de la columna que provocó la infracción de la restricción de clave externa o las filas que contienen los errores de integridad referencial. Por ejemplo, si se cambia la clave de dimensión de un atributo que no tiene datos únicos o estos son de tipo NULL, se quitan todos los datos existentes en la tabla de clave externa. Además, al quitar todos los datos de una tabla puede producirse un efecto cascada y generar otras infracciones de la integridad referencial.|  
|Atributo o dimensión eliminados|Si se elimina un atributo de una dimensión, el Asistente para generar esquemas eliminará la columna asignada al atributo eliminado. Si se elimina una dimensión, el asistente eliminará la tabla asignada a la dimensión eliminada. En estos casos, el asistente quita los datos contenidos en la tabla o columna eliminada.|  
  
 El Asistente para generar esquemas muestra una advertencia antes de quitar los datos, por lo que puede cancelarse el asistente sin perder los datos. Sin embargo, el Asistente para generar esquemas no puede diferenciar las pérdidas de datos previsibles de las imprevisibles. Al ejecutar el asistente, se muestran en un cuadro de diálogo las tablas y columnas que contienen los datos que se van a quitar. Puede continuar con el asistente y quitar los datos o cancelarlo y comprobar los cambios realizados en las tablas y columnas.  
  
## <a name="supporting-cube-and-dimension-changes"></a>Admitir cambios en un cubo o dimensión  
 Al cambiar las propiedades de las dimensiones y cubos, el Asistente para generar esquemas vuelve a generar los objetos adecuados en la base de datos del área de asunto subyacente y en la vista de origen de datos relacionada, tal como se describe en la siguiente tabla.  
  
 Eliminar un objeto, como una dimensión, un cubo o un atributo  
 El Asistente para generar esquemas elimina los objetos subyacentes a los que se asigna el objeto eliminado. Si se agregan columnas a una tabla generada por el asistente, las nuevas columnas no evitan que se elimine la tabla. Al eliminar un objeto, se quitan los datos almacenados en los objetos subyacentes y podrían quitarse también otros datos si se produjesen errores de integridad referencial.  
  
 Cambiar el nombre de un objeto, como una dimensión, un cubo o un atributo  
 El Asistente para generar esquemas cambia el nombre de los objetos subyacentes a los que se asigna el objeto cuyo nombre se ha cambiado. El asistente también cambia el nombre de los objetos afectados, como las claves principales. Se conservan los datos existentes almacenados en los objetos subyacentes.  
  
 Modificar un objeto, como cambiar el tipo de datos  
 El Asistente para generar esquemas modifica los objetos subyacentes a los que se asigna el objeto que se ha cambiado. Se conservan los datos existentes almacenados en los objetos subyacentes, a menos que el nuevo tipo de datos sea incompatible con los datos existentes.  
  
 Agregar un nuevo objeto, como una dimensión, un cubo o un atributo  
 El Asistente para generar esquemas agrega los objetos subyacentes a los que se asigna el nuevo objeto.  
  
 Si el Asistente para generar esquemas no puede realizar el cambio requerido debido a la presencia de un objeto de usuario en la base de datos del área de asunto (ya que el motor de base de datos devolvería un error), el Asistente para generar esquemas experimentará un error y se mostrará el error que devuelve el motor de base de datos. Por ejemplo, si crea una restricción de clave principal o un índice no clúster en una tabla después de que el asistente haya generado la tabla, el Asistente para generar esquemas no quita esa tabla porque no creó la restricción ni el índice.  
  
## <a name="supporting-schema-changes"></a>Admitir cambios de esquema  
 Si se cambian las propiedades de las tablas y columnas de la base de datos del área de asunto o de la vista de origen de datos asociada, el Asistente para generar esquemas trata los cambios tal como se describe en la siguiente tabla.  
  
 Eliminar una tabla o columna generada por el Asistente para generar esquemas  
 Si se elimina una tabla o columna generada por el Asistente para generar esquemas, el asistente vuelve a generar la tabla eliminada. El asistente no muestra advertencias de que se volverá a generar la tabla o columna eliminada.  
  
 Cambiar las propiedades de una tabla o columna generada por el Asistente para generar esquemas  
 Si se modifican las propiedades de una tabla o columna generada por el Asistente para generar esquemas, el asistente vuelve a generar la tabla modificada sin el cambio. Por ejemplo, si se cambia el tipo de datos, la nulabilidad de una columna o el grupo de archivos generado por el Asistente para generar esquemas, no se conservará el cambio tras la regeneración. El asistente no muestra advertencias de que se volverá a generar el objeto modificado sin el cambio.  
  
 Agregar una columna a una tabla generada por el Asistente para generar esquemas o agregar una tabla a la base de datos del área de asunto o a la base de datos del área de ensayo.  
 Si se agrega una columna a la tabla generada por el Asistente para generar esquemas, el asistente conserva la columna adicional junto con los datos almacenados en ella durante la regeneración. Sin embargo, si se agrega una tabla a la base de datos del área de asunto o a la base de datos del área de ensayo, el Asistente para generar esquemas no incorporará la nueva tabla. La columna agregada y la tabla agregada no se reflejarán en el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , en la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , en los paquetes DTS, en la vista de origen de datos ni en ninguna otra ubicación del esquema generado.  
  
## <a name="supporting-data-source-and-data-source-view-changes"></a>Admitir cambios en el origen de datos y en la vista de origen de datos  
 Si se vuelve a ejecutar el Asistente para generar esquemas, éste volverá a utilizar el mismo origen de datos y vista del origen de datos que en la generación original. Si se agrega un origen de datos o una vista de origen de datos, el asistente no los utilizará. Si se elimina el origen de datos o la vista de origen de datos originales tras la generación inicial, debe ejecutarse el asistente desde el principio. También se eliminará la configuración anterior del asistente. Los objetos existentes en una base de datos subyacente enlazados a un origen de datos o vista de origen de datos eliminados se tratarán como objetos creados por el usuario la próxima vez que se ejecute el Asistente para generar esquemas.  
  
 Si la vista de origen de datos no refleja el estado actual de la base de datos subyacente en el momento de la generación, el Asistente para generar esquemas podría registrar errores al generar los esquemas de la base de datos del área de asunto y de la base de datos del área de ensayo. Por ejemplo, si la vista de origen de datos especifica que el tipo de datos de una columna es `int`, pero el tipo de datos de la columna es en realidad `string`, el Asistente para generar esquemas establecerá `int` como tipo de datos de la clave externa para coincidir con la vista de origen de datos, pero se producirá un error al crear la relación porque el tipo de datos real es `string`.  
  
 Por otra parte, no se generarán errores si se cambia la cadena de conexión de origen de datos a una base de datos distinta de la generación anterior. Se utilizará la nueva base de datos y no se realizarán cambios en la base de datos anterior.  
  
## <a name="see-also"></a>Vea también  
 [Administrar los cambios de las vistas del origen de datos y los orígenes de datos](manage-changes-to-data-source-views-and-data-sources.md)   
 [Asistente para generar esquemas &#40;Analysis Services&#41;](schema-generation-wizard-analysis-services.md)  
  
  
