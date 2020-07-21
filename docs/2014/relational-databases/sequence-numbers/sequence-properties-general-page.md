---
title: Propiedades de secuencia (página General) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.sequence.general.f1
ms.assetid: 0187f413-cdf0-48a2-b2e6-9b3578cd5811
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6fc969dc09663da8150461529ad1e1f1fb094539
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055332"
---
# <a name="sequence-properties-general-page"></a>Propiedades de secuencia (página General)
  Crea un objeto de secuencia y especifica sus propiedades. Una secuencia es un objeto enlazado a un esquema definido por el usuario que genera una secuencia de valores numéricos según la especificación con la que se creó la secuencia. La secuencia de valores numéricos se genera en orden ascendente o descendente en un intervalo definido y se puede configurar para reiniciarse (en un ciclo) cuando se agota. Las secuencias, a diferencia de las columnas de identidad, no se asocian a tablas concretas. Las aplicaciones hacen referencia a un objeto de secuencia para recuperar su valor siguiente. La aplicación controla la relación entre las secuencias y tablas. Las aplicaciones de usuario pueden hacer referencia un objeto de secuencia y coordinar los valores a través de varias filas y tablas.  
  
 A diferencia de los valores de columnas de identidad que se generan en el momento en que se insertan filas, una aplicación puede obtener el número de secuencia siguiente sin insertar la fila llamando a la [función NEXT VALUE FOR](/sql/t-sql/functions/next-value-for-transact-sql). Use [sp_sequence_get_range](/sql/relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql) para obtener varios números de secuencia a la vez.  
  
 Para obtener información sobre las funciones **CREATE SEQUENCE** y **NEXT VALUE FOR** y escenarios en los que se usan, vea [Números de secuencia](sequence-numbers.md).  
  
 Se puede obtener acceso a esta página de dos formas: haciendo clic con el botón derecho en **Secuencias** en el Explorador de objetos y haciendo clic en **Nueva secuencia**, o haciendo clic con el botón derecho en una secuencia existente y haciendo clic en **Propiedades**. Cuando se hace clic con el botón derecho en una secuencia existente y se hace clic en **Propiedades**, no se pueden editar las opciones. Para cambiar las opciones de secuencia use la instrucción [ALTER SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-sequence-transact-sql) o quite y vuelva a crear el objeto de secuencia.  
  
## <a name="options"></a>Opciones  
 **Nombre de secuencia**  
 Escriba aquí el nombre de la secuencia.  
  
 **Esquema de secuencia**  
 Especifique el esquema que será el propietario de este flujo.  
  
 **Tipo de datos**  
 Una secuencia se puede definir como de cualquier tipo entero. Esto incluye:  
  
|Tipo de datos|Intervalo|  
|---------------|-----------|  
|`tinyint`|De 0 a 255|  
|`smallint`|De -32 768 a 32 767|  
|`int`|De -2.147.483.648 a 2.147.483.647|  
|`bigint`|De -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807|  
  
-   `decimal` o `numeric` con una escala de 0.  
  
-   Cualquier tipo de datos definido por el usuario (tipo de alias) que se base en estos tipos.  
  
 **Precisión**  
 Para los tipos de datos `decimal` o `numeric`, especifique la precisión. (La escala siempre es 0).  
  
 **Valor inicial**  
 El primer valor que el objeto de secuencia devolverá. El valor **START** debe ser menor o igual que el máximo, y mayor o igual que el valor mínimo del objeto de secuencia. El valor inicial predeterminado para un nuevo objeto de secuencia es el valor mínimo para un objeto de secuencia ascendente y el valor máximo para uno descendente.  
  
 **Incrementar en**  
 Valor que se usa para incrementar (o disminuir si es negativo) el valor del objeto de secuencia para cada llamada a la función **NEXT VALUE FOR** . Si el incremento es un valor negativo el objeto de secuencia es descendente, de lo contrario, es ascendente. El incremento no puede ser 0.  
  
 **Valor mínimo**  
 Especifica los límites del objeto de secuencia. El valor mínimo predeterminado para un nuevo objeto de secuencia es el valor mínimo del tipo de datos del objeto de secuencia. Es cero para el tipo de datos `tinyint` y un número negativo para todos los demás.  
  
 **Valor máximo**  
 Especifica los límites del objeto de secuencia. El valor máximo predeterminado para un nuevo objeto de secuencia es el valor máximo del tipo de datos del objeto de secuencia.  
  
 **La secuencia de ciclos se reiniciará al llegar al límite**  
 Seleccione el objeto de secuencia para permitir el reinicio a partir del valor mínimo (o máximo para objetos de secuencia descendente) cuando se supere su valor mínimo o máximo.  
  
> [!NOTE]  
>  Los ciclos no se reinician a partir del valor inicial, sino a partir del valor mínimo o máximo.  
  
 **Opciones de caché**  
 La creación de una memoria caché de valores de secuencia puede incrementar el rendimiento de las aplicaciones que usen objetos de secuencia minimizando el número de las E/S de disco requeridas para crear números de secuencia.  
  
-   Tamaño de memoria caché predeterminado: el [!INCLUDE[ssDE](../../includes/ssde-md.md)] seleccionará un tamaño, pero los usuarios no deben confiar en que la selección sea coherente. [!INCLUDE[msCoName](../../includes/msconame-md.md)] puede cambiar el método de cálculo del tamaño de la memoria caché sin previo aviso.  
  
-   Sin memoria caché: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no almacenará en la memoria caché los números de secuencia.  
  
-   Memoria caché con tamaño: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] almacenará en la memoria caché los valores de secuencia. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] realiza el seguimiento del valor actual y del número de valores que queden en la memoria caché. Por consiguiente, la cantidad de memoria necesaria para almacenar la memoria caché siempre es dos veces la del tipo de datos del objeto de secuencia  
  
 Cuando se crea con la opción CACHE, un cierre inesperado, como un error de alimentación, puede perder los números de secuencia de la memoria caché.  
  
 Para obtener información adicional sobre las opciones de creación de secuencias, vea [CREATE SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-sequence-transact-sql).  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **CREATE SEQUENCE**, **ALTER**o **CONTROL** en el SCHEMA.  
  
## <a name="see-also"></a>Consulte también  
 [sys.sequences &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sequences-transact-sql)  
  
  
