---
title: Propiedades de columna (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.designers.properties.Column.ColumnIdentitySpec
- vdt.designers.properties.Column
- vdt.tablecolumn
- vdt.designers.properties.Column.ColumnComputedColumnSpec
- vdt.designers.properties.Column.ColumnFulltextSpec
ms.assetid: e549a2a8-4154-4ec8-b146-614564169b39
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ef372c7a1716fe9e928b3567c52c654268f7a3e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="column-properties-visual-database-tools"></a>Propiedades de columna (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Hay dos conjuntos de propiedades para columnas: un conjunto completo que se puede ver en la pestaña **Propiedades de columna** del Diseñador de tablas (solo disponible para las bases de datos de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]) y un subconjunto que se puede ver en la ventana Propiedades con el Explorador de servidores.  
  
> [!NOTE]  
> Las propiedades de este tema se ordenan por categoría en lugar de alfabéticamente.  
  
> [!NOTE]  
> Los cuadros de diálogo y comandos de menú que ve podrían diferir de aquellos que se describen en la Ayuda en función de la edición o configuración activa. Para cambiar la configuración, elija **Importar y exportar configuraciones** en el menú **Herramientas** .  
  
## <a name="properties-window"></a>Ventana Propiedades  
Estas propiedades aparecen en la ventana Propiedades cuando selecciona una columna en el Explorador de servidores.  
  
> [!NOTE]  
> Estas propiedades, a las que se tiene acceso con el Explorador de servidores, son de solo lectura. Para editar las propiedades de columna de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , seleccione la columna en el Diseñador de tablas. Dichas propiedades se describen posteriormente en este tema.  
  
**Categoría Identidad**  
Se expande para mostrar las propiedades de **Nombre** y **Base de datos** .  
  
**Nombre**  
Muestra el nombre de la columna.  
  
**Base de datos**  
Muestra el nombre del origen de datos para la columna seleccionada. (Solo se aplica a OLE DB.)  
  
**Categoría Varios**  
Se expande para mostrar las propiedades restantes.  
  
**Tipo de datos**  
Muestra el tipo de datos de la columna seleccionada. Para obtener más información, vea [Tipos de datos (Transact-SQL)](http://msdn.microsoft.com/en-us/a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4).  
  
**Incremento de identidad**  
Muestra el incremento que se agregará a la **Inicialización de identidad** para cada fila posterior de la columna de identidad. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**Inicialización de identidad**  
Muestra el valor de inicialización asignado a la primera fila de la tabla para la columna de identidad. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**Identidad**  
Muestra si la columna seleccionada es la columna de identidad de la tabla. (Solo se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**Longitud**  
Muestra el número de caracteres permitidos para los tipos de datos basados en caracteres.  
  
**Admisión de valores NULL**  
Muestra si la columna permite o no valores NULL.  
  
**Precisión**  
Muestra el número máximo de dígitos admitido para tipos de datos numéricos. Esta propiedad muestra **0** para tipos de datos no numéricos.  
  
**Escala**  
Muestra el número máximo de dígitos que pueden aparecer a la derecha del separador decimal para los tipos de datos numéricos. Este valor debe ser menor o igual que la precisión. Esta propiedad muestra **0** para tipos de datos no numéricos.  
  
## <a name="column-properties-tab"></a>Pestaña Propiedades de columna  
Para tener acceso a estas propiedades, en el Explorador de servidores haga clic con el botón derecho en la tabla a la que pertenece la columna, elija **Abrir definición de tabla**y seleccione la fila en la cuadrícula de tabla en el Diseñador de tablas.  
  
> [!NOTE]  
> Estas propiedades solo se aplican a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Categoría General**  
Se expande para mostrar **Nombre**, **Permitir valores NULL**, **Tipo de datos**, **Valor o enlace predeterminado**, **Longitud**, **Precisión**y **Escala**.  
  
**Nombre**  
Muestra el nombre de la columna. Para editar el nombre, escriba en el cuadro de texto.  
  
> [!CAUTION]  
> Si hay consultas, vistas, funciones definidas por el usuario, procedimientos almacenados o programas existentes que hacen referencia a la columna, la modificación del nombre hará que estos objetos no sean válidos.  
  
**Permitir valores NULL**  
Muestra si el tipo de datos de la columna admite o no los valores NULL.  
  
**Tipo de datos**  
Muestra el tipo de datos de la columna seleccionada. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor. Para obtener más información, vea [Tipos de datos (Transact-SQL)](http://msdn.microsoft.com/en-us/a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4).  
  
**Valor o enlace predeterminado**  
Muestra el valor predeterminado de esta columna cuando no se especifica ningún valor para esta columna. La lista desplegable contiene todos los valores predeterminados globales definidos en el origen de datos. Para enlazar la columna con un valor predeterminado global, realice una selección en la lista desplegable. Otra opción para crear una restricción predeterminada para la columna es escribir directamente el valor predeterminado como texto.  
  
**Longitud**  
Muestra el número de caracteres permitidos para los tipos de datos basados en caracteres. Esta propiedad solo está disponible para tipos de datos basados en caracteres.  
  
**Precisión**  
Muestra el número máximo de dígitos admitido para tipos de datos numéricos. Esta propiedad muestra **0** para tipos de datos no numéricos. Esta propiedad solo está disponible para tipos de datos numéricos.  
  
**Escala**  
Muestra el número máximo de dígitos que pueden aparecer a la derecha del separador decimal para los tipos de datos numéricos. Este valor debe ser menor o igual que la precisión. Esta propiedad muestra **0** para tipos de datos no numéricos. Esta propiedad solo está disponible para tipos de datos numéricos.  
  
**Categoría Diseñador de tablas**  
Se expande para mostrar las propiedades restantes.  
  
**Intercalación**  
Muestra la configuración de intercalación para la columna seleccionada. Para cambiar esta configuración, haga clic en **Intercalación** y, a continuación, haga clic en los puntos suspensivos **(…)** que hay a la derecha del valor.  
  
**Categoría Especificación de columna calculada**  
Esta opción se expande para mostrar propiedades para **Fórmula** y **Persistente**. Si la columna está calculada, también aparecerá la fórmula. Para editar la fórmula, amplíe esta categoría y edítela en la propiedad **Fórmula** .  
  
**Fórmula**  
Muestra la fórmula que utiliza la columna seleccionada si es una columna calculada. En este campo puede escribir o cambiar una fórmula.  
  
**Persistente**  
Le permite guardar la columna calculada con el origen de datos. Una columna calculada mantenida se puede indizar.  
  
**Tipo de datos comprimido**  
Muestra información sobre el tipo de datos del campo con el mismo formato que la instrucción SQL CREATE TABLE. Por ejemplo, un campo que contiene una cadena de longitud variable con una longitud máxima de 20 caracteres se representa como "varchar(20)". Para cambiar esta propiedad, escriba el valor directamente.  
  
**Descripción**  
Muestra la descripción de la columna. Para ver la descripción completa o para editarla, haga clic en Descripción y, a continuación, haga clic en los puntos suspensivos **(…)** a la derecha de la propiedad.  
  
**Categoría Especificación de texto completo**  
Se expande para mostrar propiedades específicas para columnas de texto completo.  
  
**Está indizado por texto completo**  
Indica si esta columna está indizada con texto completo. Esta propiedad solo puede establecerse en **Sí** si el tipo de datos de la columna se puede buscar por texto completo y si la tabla a la que pertenece esta columna tiene especificado un índice de texto completo. Para cambiar este valor, haga clic en el mismo, amplíe la lista desplegable y elija otro valor.  
  
**Columna de tipo de texto completo**  
Muestra qué columna se utiliza para definir el tipo de documento de una columna de tipo imagen. Se puede utilizar el tipo de datos de imagen para almacenar documentos del intervalo de archivos .doc a archivos .xml.  
  
**Lenguaje**  
Indica el idioma empleado para indizar la columna.  
  
**Semántica estadística**  
Seleccione si desea habilitar la indización semántica estadística para la columna seleccionada. Para más información, consulte [Marcador de posición de Búsqueda semántica](http://msdn.microsoft.com/en-us/cd8faa9d-07db-420d-93f4-a2ea7c974b97).  
  
Si selecciona **Idioma** antes de seleccionar **Semántica estadística**y el idioma seleccionado no tiene un modelo de idioma semántico asociado, la opción **Semántica estadística** se establece en **No** y no puede modificarse. Si selecciona **Sí** para la opción de **Semántica estadística** antes de seleccionar **Idioma**, los idiomas disponibles en la columna **Idioma** estarán limitados a aquellos para los que exista un modelo de idioma semántico.  
  
**Suscriptor que no es de SQL Server**  
Muestra si la columna tiene un suscriptor que no es de Microsoft SQL Server.  
  
**Categoría Especificación de identidad**  
Esta opción se expande para mostrar las propiedades **Identidad**, **Incremento de identidad**e **Inicialización de identidad**.  
  
**Identidad**  
Muestra si la columna seleccionada es la columna de identidad de la tabla. Para cambiar la propiedad, abra la tabla en el Diseñador de tablas y edite las propiedades en la ventana **Propiedades** . Esta configuración solo se aplica a las columnas con un tipo de datos basado en números, como *int*.  
  
**Incremento de identidad**  
Muestra el incremento que se agregará a la **Inicialización de identidad** para cada fila subsiguiente. Si deja esta celda en blanco, se le asignará el valor 1 de forma predeterminada. Para editar esta propiedad, escriba el nuevo valor directamente.  
  
**Inicialización de identidad**  
Muestra el valor asignado a la primera fila de la tabla. Si deja esta celda en blanco, se le asignará el valor 1 de forma predeterminada. Para editar esta propiedad, escriba el nuevo valor directamente.  
  
**Determinístico**  
Muestra si se puede determinar con exactitud el tipo de dato de la columna seleccionada.  
  
**Publicado por DTS**  
Muestra si la columna está publicada con DTS.  
  
**Indizable**  
Muestra si la columna seleccionada se puede indizar. Por ejemplo, no se pueden indizar las columnas calculadas no deterministas.  
  
**Publicado por combinación**  
Muestra si la columna está publicada por combinación.  
  
**No disponible para replicación**  
Indica si los valores de identidad originales se conservan durante la replicación. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor.  
  
**Replicado**  
Muestra si esta columna se replica en otra ubicación.  
  
**RowGuid**  
Indica si [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usa la columna como ROWGUID. Puede establecer este valor en **Sí** solo para una columna con el tipo de datos **uniqueidentifier**. Para editar esta propiedad, haga clic en su valor, expanda la lista desplegable y elija otro valor.  
  
**Tamaño**  
Muestra el tamaño en bytes permitido por el tipo de datos de la columna. Por ejemplo, un tipo de datos **nchar** puede tener una longitud de 10 (número de caracteres) pero tendría un tamaño de 20 para los juegos de caracteres Unicode.  
  
> [!NOTE]  
> La longitud de un tipo de datos **varchar(max)** varía en cada fila. sp_help devuelve (-1) como la longitud de la columna **varchar(max)** . [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] muestra -1 como tamaño de columna.  
  
