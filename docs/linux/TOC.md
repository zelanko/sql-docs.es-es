# [Acerca de SQL Server en Linux](sql-server-linux-overview.md)

# Información general
## [Notas de la versión](sql-server-linux-release-notes.md)
## [Novedades de esta versión](sql-server-linux-whats-new.md)
## [Artículos nuevos y actualizados](new-updated-linux.md)
## [Ediciones y características admitidas](sql-server-linux-editions-and-components-2017.md)

# Tutoriales rápidos
## [Instalación y conexión: Red Hat](quickstart-install-connect-red-hat.md)
## [Instalación y conexión: SUSE](quickstart-install-connect-suse.md)
## [Instalación y conexión: Ubuntu](quickstart-install-connect-ubuntu.md)
## [Ejecución y conexión: Docker](quickstart-install-connect-docker.md)
## [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
## [Ejecución y conexión: nube](quickstart-install-connect-clouds.md)

# Tutoriales
## [1_Migración desde Windows](sql-server-linux-migrate-restore-database.md)
## [2_Migración desde Oracle](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)
## [3_Migración a Docker](tutorial-restore-backup-in-sql-server-container.md)
## [4_Creación de un trabajo](sql-server-linux-run-sql-server-agent-job.md)
## [5_Configuración de Autenticación de AD](sql-server-linux-active-directory-authentication.md)
## [6_Creación de una instancia de clúster de conmutación por error](sql-server-linux-shared-disk-cluster-configure.md)
### [iSCSI](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
### [NFS](sql-server-linux-shared-disk-cluster-configure-nfs.md)
### [SMB](sql-server-linux-shared-disk-cluster-configure-smb.md)

# Conceptos
## Install
### [Instalar SQL Server](sql-server-linux-setup.md)
### [Instalar Herramientas de SQL Server](sql-server-linux-setup-tools.md)
### [Instalar el Agente SQL Server](sql-server-linux-setup-sql-agent.md)
### [Instalar Búsqueda de texto completo de SQL Server](sql-server-linux-setup-full-text-search.md)
### [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)
### [Registrar repositorio GA](sql-server-linux-change-repo.md)

## Configurar
### [Configuración con mssql-conf](sql-server-linux-configure-mssql-conf.md)
### [Variables de entorno](sql-server-linux-configure-environment-variables.md)
### [Configuración de contenedores de Docker](sql-server-linux-configure-docker.md)
### [Comentarios del cliente](sql-server-linux-customer-feedback.md)

## [Desarrollo](sql-server-linux-develop-overview.md)
### [Bibliotecas de conectividad](sql-server-linux-develop-connectivity-libraries.md)
### [Usar Visual Studio Code](sql-server-linux-develop-use-vscode.md)
### [Usar SSMS](sql-server-linux-develop-use-ssms.md)
### [Usar SSDT](sql-server-linux-develop-use-ssdt.md)

## [Administrar](sql-server-linux-management-overview.md)
### [Usar SSMS para administrar](sql-server-linux-manage-ssms.md)
### [Usar PowerShell para administrar](sql-server-linux-manage-powershell.md)
### [Usar el trasvase de registros](sql-server-linux-use-log-shipping.md)
### [Usar alertas de correo electrónico y de correo de base de datos](sql-server-linux-db-mail-sql-agent.md)

## [Migrar](sql-server-linux-migrate-overview.md)
### [Exportar e importar un BACPAC desde Windows](sql-server-linux-migrate-ssms.md)
### [Migrar con SQL Server Migration Assistant](sql-server-linux-migrate-ssma.md)
### [Copia masiva con bcp](sql-server-linux-migrate-bcp.md)

## [Extracción, transformación y carga](sql-server-linux-migrate-ssis.md)
### [Limitaciones y problemas conocidos](sql-server-linux-ssis-known-issues.md)
### [Configurar SSIS](sql-server-linux-configure-ssis.md)
### [Programar paquetes de SSIS](sql-server-linux-schedule-ssis-packages.md)

## [Configurar la continuidad empresarial](sql-server-linux-business-continuity-dr.md)
### [Copias de seguridad y restauración](sql-server-linux-backup-and-restore-database.md)
#### [Interfaz de dispositivo virtual: Linux](sql-server-linux-backup-vdi-specification.md)
### [Instancia de clúster de conmutación por error](sql-server-linux-shared-disk-cluster-concepts.md)
#### [Red Hat Enterprise Linux]()
##### [Configurar (complemento de alta disponibilidad)](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)
##### [Operar (complemento de alta disponibilidad)](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
#### [SUSE Linux Enterprise Server]()
##### [Configurar (complemento de alta disponibilidad)](sql-server-linux-shared-disk-cluster-sles-configure.md)
### [Grupos de disponibilidad](sql-server-linux-availability-group-overview.md)
#### [Crear para la alta disponibilidad](sql-server-linux-availability-group-ha.md)
##### [Configurar un grupo de disponibilidad](sql-server-linux-availability-group-configure-ha.md)
##### [Configurar en RHEL](sql-server-linux-availability-group-cluster-rhel.md)
##### [Configurar en SUSE](sql-server-linux-availability-group-cluster-sles.md)
##### [Configurar en Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)
##### [Operar](sql-server-linux-availability-group-failover-ha.md)
#### [Crear solo para el escalado de lectura]()
##### [Configurar un grupo de disponibilidad](sql-server-linux-availability-group-configure-rs.md)

## [Seguridad](sql-server-linux-security-overview.md)
### [Empezar a trabajar con las características de seguridad](sql-server-linux-security-get-started.md)
### [Cifrado de conexiones](sql-server-linux-encrypted-connections.md)

## Rendimiento
### [Procedimientos recomendados](sql-server-linux-performance-best-practices.md)
### [Introducción a las características de rendimiento](sql-server-linux-performance-get-started.md)

# Ejemplos
## Instalación desatendida
### [Red Hat Enterprise Linux](sample-unattended-install-redhat.md)
### [SUSE Linux Enterprise Server](sample-unattended-install-suse.md)
### [Ubuntu](sample-unattended-install-ubuntu.md)

# Recursos
## [Solucionar problemas](sql-server-linux-troubleshooting-guide.md)
## [Documentación de SQL Server](../sql-server/sql-server-technical-documentation.md)
## Asociados
### [Supervisión](../sql-server/partner-monitor-sql-server.md)
### [Alta disponibilidad y recuperación ante desastres](../sql-server/partner-hadr-sql-server.md)
### [Administración](../sql-server/partner-management-sql-server.md)
### [Desarrollo](../sql-server/partner-dev-sql-server.md)
## [Cambio de la pila DBA](https://dba.stackexchange.com/questions/tagged/sql-server)
## [Desbordamiento de pila](http://stackoverflow.com/questions/tagged/sql-server)
## [Foros de MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
## [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)
## [Reddit](https://www.reddit.com/r/SQLServer)
