---
title: Arquitectura y administración de registros de transacciones de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 4d1a4f97-3fe4-44af-9d4f-f884a6eaa457
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 2495b9487a633fff6c5214a07e589f58fafa5e61
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "62512768"
---
# <a name="sql-server-transaction-log-architecture-and-management"></a>Arquitectura y administración de registros de transacciones de SQL Server

[!INCLUDE[appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Todas las bases de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tienen un registro de transacciones que graba todas las transacciones y las modificaciones que cada transacción realiza en la base de datos. El registro de transacciones es un componente esencial de la base de datos y, si se produce un error del sistema, podría ser necesario para volver a poner la base de datos en un estado coherente. Esta guía proporciona información acerca de la arquitectura física y lógica del registro de transacciones. Comprender la arquitectura puede mejorar la eficacia en la administración de registros de transacciones.  

  
##  <a name="transaction-log-logical-architecture"></a><a name="Logical_Arch"></a>Arquitectura lógica del registro de transacciones  

 El registro de transacciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] funciona desde el punto de vista lógico como si fuese una cadena de entradas de registro. Cada entrada del registro está identificada por un número de flujo de registro (LSN, Log Sequence Number). Las nuevas entradas del registro se escriben al final lógico del registro con un LSN mayor que el de las entradas anteriores. Las entradas del registro se almacenan en la secuencia en la que se crean. Cada entrada del registro contiene el Id. de la transacción a la que pertenece. Por cada transacción, las entradas del registro asociadas a dicha transacción se vinculan individualmente en una cadena con punteros hacia atrás, para acelerar así la reversión de la transacción.  
  
 Los registros de modificaciones de datos registran la operación lógica llevada a cabo o las imágenes anterior y posterior de los datos modificados. La imagen anterior es una copia de los datos antes de llevar a cabo la operación; la imagen posterior es una copia de los datos después de haber realizado la operación.  
  
 Los pasos para recuperar una operación dependen del tipo de registro:  
  
-   Registro de la operación lógica  
  
    -   Para poner al día la operación lógica, se vuelve a ejecutar la operación.  
  
    -   Para revertir la operación lógica, se ejecuta la operación lógica inversa.  
  
-   Registro de las imágenes anterior y posterior  
  
    -   Para poner al día la operación, se aplica la imagen posterior.  
  
    -   Para revertir la operación, se aplica la imagen anterior.  
  
 En el registro de transacciones se registran muchos tipos de operaciones. Entre las operaciones se incluyen:  
  
-   El inicio y el final de cada transacción.  
  
-   Todas las modificaciones de los datos (inserción, actualización y eliminación). Esto incluye las modificaciones de las tablas, incluidas las tablas del sistema, hechas por procedimientos almacenados del sistema o por instrucciones del lenguaje de definición de datos (DDL).  
  
-   Las asignaciones o cancelaciones de asignación de páginas y extensiones.  
  
-   La creación o eliminación de una tabla o un índice.  
  
 También se registran las operaciones de reversión. Cada transacción reserva espacio en el registro de transacciones para asegurarse de que existe suficiente espacio de registro para admitir una reversión provocada por una instrucción de reversión explícita o cuando se produce un error. La cantidad de espacio reservado depende de las operaciones realizadas en la transacción, pero normalmente equivale a la cantidad de espacio empleado para registrar cada operación. Este espacio reservado se libera cuando se completa la transacción.  
  
  La sección del archivo de registro a partir de la primera entrada de registro que debe estar presente para una reversión correcta en toda la base de datos hasta la última entrada de registro escrita se denomina parte activa del registro o *registro activo*. Esta es la sección del registro necesaria para una recuperación completa de la base de datos. No se puede truncar ninguna parte del registro activo. El número de secuencia de registro (LSN) de este primer registro se denomina el LSN de recuperación mínimo (*MinLSN*).  
  
##  <a name="transaction-log-physical-architecture"></a><a name="physical_arch"></a> Arquitectura física del registro de transacciones  

 El registro de transacciones de una base de datos está asignado a uno o varios archivos físicos. Conceptualmente, el archivo de registro es una cadena de entradas de registro. Físicamente, la secuencia de entradas del registro se almacena de forma eficaz en el conjunto de archivos físicos que implementa el registro de transacciones. Cada base de datos debe tener al menos un archivo de registro.  
  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] segmenta cada archivo de registro físico internamente en una serie de archivos de registro virtuales. Los archivos de registro virtuales no tienen un tamaño fijo y no hay un número fijo de archivos de registro virtuales para un archivo de registro físico. [!INCLUDE[ssDE](../includes/ssde-md.md)] elige dinámicamente el tamaño de los archivos de registro virtuales al crear o ampliar los archivos de registro. [!INCLUDE[ssDE](../includes/ssde-md.md)] intenta mantener un número reducido de archivos virtuales. El tamaño de los archivos virtuales después de ampliar un archivo de registro equivale a la suma del tamaño del registro existente y el tamaño del nuevo incremento del archivo. El tamaño o número de archivos de registro virtuales no lo pueden configurar ni establecer los administradores.  
  
 Los archivos de registro virtuales solo afectan al rendimiento del sistema si se definen archivos de registros físicos mediante valores pequeños para *size* y *growth_increment* . El valor *size* es el tamaño inicial del archivo de registro y el valor de *growth_increment* es la cantidad de espacio que se agrega al archivo cada vez que se necesita más espacio. Si los archivos de registro crecen hasta un tamaño grande debido a muchos incrementos pequeños, tendrán numerosos archivos de registro virtuales. Esto puede retrasar el inicio de la base de datos, así como las operaciones de copias de seguridad y restauración del registro. Se recomienda que los archivos de registro se definan con un valor *size* cercano al tamaño final necesario y que tengan también un valor de *growth_increment* relativamente alto. Para obtener más información sobre estos parámetros, consulte [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).  
  
 El registro de transacciones es un archivo de registro circular. Considere, por ejemplo, una base de datos con un archivo de registro físico dividido en cuatro archivos de registros virtuales. Cuando se crea la base de datos, el archivo de registro lógico empieza en el principio del archivo de registro físico. Las nuevas entradas del registro se agregan al final del registro lógico y se expanden hacia el final del archivo físico. El truncamiento del registro libera los registros virtuales cuyas entradas son anteriores al número de flujo de registro de recuperación mínimo (MinLSN). *MinLSN* es el número de flujo de registro de la entrada del registro más antigua necesaria para una reversión correcta de toda la base de datos. El registro de transacciones de ejemplo sería similar al de la siguiente ilustración.  
  
 ![Archivo de registro dividido en cuatro archivos de registro virtuales](media/tranlog3.gif "Archivo de registro dividido en cuatro archivos de registro virtuales")  
  
 Cuando el final del registro lógico llega al final del archivo de registro físico, las nuevas entradas del registro se escriben al principio del archivo de registro físico.  
  
 ![Las entradas de registro saltan al inicio del archivo de registro](media/tranlog4.gif "Las entradas de registro saltan al inicio del archivo de registro")  
  
 El ciclo se repite indefinidamente, siempre que el final del registro lógico no alcance el inicio del registro lógico. Si las entradas antiguas se truncan con la frecuencia suficiente para disponer siempre de espacio para todas las nuevas entradas de registro que se van a crear hasta el próximo punto de comprobación, el registro no se llena nunca. Sin embargo, si el final del registro lógico llega al principio del registro lógico, se produce una de estas dos situaciones:  
  
-   Si el registro tiene habilitada la opción FILEGROWTH y hay espacio disponible en el disco, el archivo se amplía en la cantidad especificada en el parámetro *growth_increment* y las nuevas entradas del registro se escriben en la extensión. Para obtener más información sobre la opción FILEGROWTH, consulte [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).  
  
-   Si la opción FILEGROWTH no está habilitada o el disco que almacena el archivo de registro tiene menos espacio disponible que la cantidad especificada en *growth_increment*, se genera el error 9002.  
  
 Si el registro contiene varios archivos de registro físicos, el registro lógico pasará por todos los archivos de registro físicos antes de volver a empezar por el principio del primer archivo de registro físico.  
  
### <a name="log-truncation"></a>Truncamiento del registro  

 El truncamiento del registro es esencial para evitar que se llene. El truncamiento del registro elimina los archivos de registro virtuales inactivos del registro de transacciones lógico de una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , liberando espacio en el registro lógico para que lo reutilice el registro de transacciones físico. Si no se truncara nunca un registro de transacciones, acabaría ocupando todo el espacio de disco asignado a sus archivo de registro físicos. Sin embargo, para que se pueda truncar el registro, se debe realizar primero una operación de punto de comprobación. Un punto de comprobación escribe en el disco las páginas modificadas en memoria actuales (denominadas páginas desfasadas) y la información del registro de transacciones de la memoria. Cuando se lleva a cabo el punto de comprobación, la parte inactiva del registro de transacciones se marca como reutilizable. A partir de ese momento, se puede liberar la parte inactiva mediante el truncamiento del registro. Para obtener más información sobre los puntos de comprobación, consulte [Puntos de comprobación de base de datos &#40;SQL Server&#41;](../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 En la siguiente ilustración se muestra un registro de transacciones antes y después del truncamiento. En la primera ilustración se muestra un registro de transacciones que no se ha truncado nunca. El registro lógico tiene actualmente cuatro archivos de registro virtuales en uso. El registro lógico comienza al principio del primer archivo de registro virtual y finaliza en el registro virtual 4. El registro de MinLSN está en el registro virtual 3. Los registros virtuales 1 y 2 solo contienen entradas de registro inactivas. Estas entradas pueden truncarse. El registro virtual 5 no se utiliza aún y no forma parte del registro lógico actual.  
  
 ![Registro de transacciones con cuatro registros virtuales](media/tranlog2.gif "Registro de transacciones con cuatro registros virtuales")  
  
 En la segunda ilustración se muestra el registro después del truncamiento. Se han liberado los registros virtuales 1 y 2 para su reutilización. El registro lógico comienza ahora al principio del registro virtual 3. El registro virtual 5 no se utiliza aún y no forma parte del registro lógico actual.  
  
 ![Archivo de registro dividido en cuatro archivos de registro virtuales](media/tranlog3.gif "Archivo de registro dividido en cuatro archivos de registro virtuales")  
  
 El truncamiento del registro se produce automáticamente después de los eventos siguientes, excepto cuando se retrasa por alguna razón:  
  
-   En el modelo de recuperación simple, después de un punto de comprobación.  
  
-   Bajo el modelo de recuperación completa o el modelo de recuperación optimizado para cargas masivas de registros, después de una copia de seguridad del registro, si un punto de comprobación ha producirse desde la copia de seguridad anterior.  
  
 El truncamiento del registro se puede retrasar por diferentes factores. En caso de un retraso largo en el truncamiento del registro, el registro de transacciones se puede llenar. Para obtener más información, vea [factores que pueden retrasar el truncamiento del registro](../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation) y [solucionar problemas de un registro de transacciones lleno &#40;SQL Server Error 9002&#41;](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
##  <a name="write-ahead-transaction-log"></a><a name="WAL"></a>Registro de transacciones de escritura previa  

 En esta sección se describe el rol que desempeña el registro de transacciones de escritura anticipada en la grabación de modificaciones de datos en disco. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa un registro de escritura anticipada (WAL) que garantiza que ninguna modificación de datos se escribe en el disco antes que la entrada de registro asociada. Así se mantienen las propiedades ACID para una transacción.  
  
 Para entender cómo funciona el registro de escritura anticipada, es importante saber cómo se escriben los datos modificados en el disco. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mantiene una caché del búfer que lee las páginas de datos cuando estos deben recuperarse. Cuando se modifica una página en la caché del búfer, no se vuelve a escribir inmediatamente en el disco; en su lugar, la página se marca como *desfasada*. Una página de datos puede tener más de una escritura lógica antes de que se escriba físicamente en el disco. Para cada escritura lógica, se inserta una entrada del registro de transacciones en la caché del registro que registra la modificación. Las entradas del registro se tienen que escribir en el disco antes de que la página desfasada asociada se quite de la caché del búfer y se escriba en el disco. El proceso de punto de comprobación examina periódicamente la caché del búfer en busca de búferes con páginas de una base de datos especificada y escribe todas las páginas desfasadas en el disco. Los puntos de comprobación permiten ahorrar tiempo en una recuperación posterior al crear un punto en el que se garantiza que todas las páginas desfasadas se hayan escrito en el disco.  
  
 A la escritura en el disco de una página de datos modificada desde la caché del búfer se le llama vaciar la página. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene una lógica que evita que una página desfasada se vacíe antes de que se escriba la entrada del registro asociada. Las entradas de registro se escriben en el disco cuando las transacciones se confirman.  
  
##  <a name="transaction-log-backups"></a><a name="Backups"></a>Copias de seguridad del registro de transacciones  

 En esta sección se presentan conceptos acerca de cómo realizar copias de seguridad y restaurar (aplicar) registros de transacciones. En los modelos de recuperación completa y de recuperación optimizada para cargas masivas de registros, es necesario realizar copias de seguridad periódicas de los registros de transacciones (*copias de seguridad de registros*) para recuperar datos. Puede realizar una copia de seguridad del registro mientras se está ejecutando cualquier copia de seguridad completa. Para obtener más información sobre modelos de recuperación, consulte [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Antes de crear la primera copia de seguridad de registros, debe crear una copia de seguridad completa, como una copia de seguridad de la base de datos o la primera de un conjunto completo de copias de seguridad de archivos. La restauración de una base de datos utilizando únicamente copias de seguridad de archivos puede llegar a ser un proceso complejo. Por lo tanto, es recomendable que comience con una copia de seguridad de la base de datos completa si es posible. Posteriormente, será necesario realizar copias de seguridad del registro de transacciones con regularidad. De esta forma, no solo se minimiza el riesgo de pérdida de trabajo, sino que también se permite el truncamiento del registro de transacciones. Normalmente, el registro de transacciones se trunca tras cada copia de seguridad de registros convencional.  
  
 Es aconsejable realizar copias de seguridad de registros suficientemente regulares para ajustarse a los requisitos de su empresa, específicamente a la tolerancia a la pérdida de trabajo que una unidad de registro dañada podría provocar. La frecuencia adecuada para realizar copias de seguridad de registros varía en función de la tolerancia al riesgo de pérdida de trabajo y, por otra parte, de la cantidad de copias de seguridad de registros que puede almacenar, administrar y, potencialmente, restaurar. Una copia de seguridad de registros cada 15 ó 30 minutos puede ser suficiente. Si su empresa necesita minimizar el riesgo de pérdida de trabajo, piense en la posibilidad de realizar copias de seguridad de registros más frecuentemente. La existencia de copias de seguridad más frecuentes de los registros tiene la ventaja añadida de aumentar la frecuencia de truncamiento del registro, lo que genera archivos de registro menores.  
  
 Para limitar el número de copias de seguridad del registro que necesita restaurar, es esencial que realice una copia de seguridad de sus datos periódicamente. Por ejemplo, podría programar una copia de seguridad completa de la base de datos cada semana y copias de seguridad diferenciales de la base de datos a diario.  
  
### <a name="the-log-chain"></a>La cadena de registros  

 Una secuencia continua de copias de seguridad de registros se denomina *cadena de registros*. Una cadena de registros empieza con una copia de seguridad completa de la base de datos. Normalmente, una cadena de registro nueva solo empieza cuando se realiza la primera copia de seguridad de la base de datos o después de que se cambie del modelo de recuperación simple al modelo de recuperación completa o al modelo de recuperación optimizado para cargas masivas de registros. A menos que se elija sobrescribir los conjuntos de copia de seguridad existentes al crear una copia de seguridad completa de la base de datos, la cadena de registros existente permanece intacta. Con la cadena de registros intacta, se puede restaurar la base de datos a partir de cualquier copia de seguridad completa de la base de datos del conjunto de medios, seguida de todas las copias de seguridad de los registros subsiguientes hasta el punto de recuperación. El punto de recuperación puede ser el final de la última copia de seguridad de registros o un punto de recuperación concreto de cualquiera de las copias de seguridad de registros. Para obtener más información, vea [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 Para restaurar una base de datos al momento del error, es preciso que la cadena de registros esté intacta. De esta forma, es necesario que una secuencia ininterrumpida de las copias de seguridad del registro de transacciones se extienda hasta el momento del error. El lugar en el que esta secuencia de registros debe comenzar depende del tipo de copias de seguridad de datos que esté restaurando: de base de datos, parcial o de archivos. En las copias de seguridad de base de datos o parciales, la secuencia de copias de seguridad de registros debe extenderse desde el final de la copia de seguridad de base de datos o parcial. En un conjunto de copia de seguridad de archivos, la secuencia de copias de seguridad de registros debe comenzar desde el principio del conjunto completo de copias de seguridad de archivos. Para obtener más información, vea [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
### <a name="restore-log-backups"></a>Restaurar copias de seguridad de registros  

 Al restaurar una copia de seguridad de registros se ponen al día los cambios que se registraron en el registro de transacciones para volver a crear el estado exacto de la base de datos en el momento en que se inició la operación de copia de seguridad de registros. Al restaurar una base de datos, será necesario restaurar las copias de seguridad de registros creadas tras la copia de seguridad de la base de datos completa que esté restaurando o al principio de la primera copia de seguridad de archivos que esté restaurando. Normalmente, se debe restaurar una serie de copias de seguridad de registros hasta llegar al punto de recuperación después de haber restaurado la copia de seguridad de los datos o la copia de seguridad diferencial más recientes. A continuación, se realiza la recuperación de la base de datos. De esta manera, todas las transacciones que estaban incompletas cuando comenzó la recuperación se revertirán y la base de datos se conectará. Una vez recuperada la base de datos, ya no es posible restaurar más copias de seguridad. Para obtener más información, vea [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
## <a name="additional-reading"></a>Lecturas adicionales  

 Se recomiendan los artículos y libros siguientes para obtener información adicional sobre el registro de transacciones.  
  
 [Descripción del registro y la recuperación en SQL Server por Paul Randall](https://technet.microsoft.com/magazine/2009.02.logging.aspx)  
  
 [Administración de registros de transacciones de SQL Server por Tony Davis y Gail Shaw](http://www.simple-talk.com/books/sql-books/sql-server-transaction-log-management-by-tony-davis-and-gail-shaw/)  
  
  
