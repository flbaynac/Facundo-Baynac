---
share: "true"
---
# [Introducción a AD DS](https://learn.microsoft.com/es-es/training/modules/introduction-to-ad-ds/)
## Componentes lógicos y físicos 
### Lógicos:
#### Partición
Una partición, o contexto de nomenclatura, es una parte de la base de datos de AD DS. Aunque la base de datos consta de un archivo denominado Ntds.dit, las diferentes particiones contienen datos diferentes. Por ejemplo, la partición de esquema contiene una copia del esquema de Active Directory
#### Schema
Un esquema es el conjunto de definiciones de los tipos de objeto y los atributos que se usan para definir los objetos creados en AD DS
#### Domain
Un dominio es un contenedor administrativo lógico para objetos como usuarios y equipos
#### Árbol de dominios
Un árbol de dominios es una colección jerárquica de dominios que comparten un dominio raíz común y un espacio de nombres del sistema de nombres de dominio (DNS) contiguo.
#### Bosque
Un bosque es una colección de uno o varios dominios que tienen una raíz AD DS común, un esquema común y un catálogo global común
#### Unidad Organizativa
Una unidad organizativa es un objeto contenedor de usuarios, grupos y equipos que proporciona un marco para la delegación de derechos administrativos y la administración mediante la vinculación de objetos de directiva de grupo (GPO)
#### Contenedor
Un contenedor es un objeto que proporciona un marco de organización para su uso en AD DS. Puede usar los contenedores predeterminados o bien crear contenedores personalizados. No se pueden vincular GPO a contenedores
### Físicos
#### Controlador de dominio
Un controlador de dominio contiene una copia de la base de datos de AD DS. Para la mayoría de las operaciones, cada controlador de dominio puede procesar los cambios y replicarlos en todos los demás controladores de dominio del dominio
#### Almacén de datos
Existe una copia del almacén de datos en cada controlador de dominio. La base de datos de AD DS usa la tecnología de base de datos Microsoft Jet y almacena la información de directorio en el archivo Ntds.dit y en los archivos de registro asociados. La carpeta `C:\Windows\NTDS` almacena estos archivos de forma predeterminada
#### Servidor del catálogo global
Un servidor del catálogo global es un controlador de dominio que hospeda el catálogo global, que es una copia parcial de solo lectura de todos los objetos de un bosque de varios dominios. Un catálogo global acelera las búsquedas de objetos que pueden estar almacenados en controladores de un dominio diferente del bosque
#### Controlador de dominio de solo lectura (`RODC`)
Un RODC es una instalación especial de solo lectura de AD DS. Los RODC son comunes en las sucursales donde la seguridad física no es óptima, el soporte de TI es menos avanzado que en los centros corporativos principales, o las aplicaciones de línea de negocio necesitan ejecutarse en un controlador de dominio
#### Sitio
Un sitio es un contenedor de objetos de AD DS, como equipos y servicios que son específicos de una ubicación física. Esto es en comparación con un dominio, que representa la estructura lógica de objetos, como usuarios y grupos, además de los equipos
#### Subnet
Una subred es una parte de las direcciones IP de la red de una organización asignada a los equipos de un sitio. Un sitio puede tener más de una subred

## Usuarios, Grupos y Equipos
### Usuarios:
#### Usuario de dominio: Principalmente contiene: 
- El nombre de usuario.
- Una contraseña de usuario.
- Pertenencias a grupos.
- También contiene parámetros que se pueden configurar en función de los requisitos de la organización. (Puesto, teléfono, etc.)
#### Cuentas de servicio administradas
Se utiliza principalmente para autentificar servicios (programas que se ejecutan en windows server) y que utilicen funcionalidades del dominio. Es símil a una cuenta local del equipo.
Windows Server admite un objeto de AD DS, denominado cuenta de servicio administrada, que se utiliza para facilitar la administración de la cuenta de servicio. Una cuenta de servicio administrada es una clase de objeto AD DS que permite:
	- Administración simplificada de contraseñas.
	- Administración simplificada de SPN ([Service Principal Name](Service%20Principal%20Name.md)).
#### Cuentas de servicio administradas de grupo (gMSA)
Se utiliza en entornos de [Clústeres de equilibrio de carga de red (NLB)](Cl%C3%BAsteres%20de%20equilibrio%20de%20carga%20de%20red%20(NLB).md) o [Internet Information Services (IIS)](Internet%20Information%20Services%20(IIS).md) para poder usar una misma cuenta de servicio administrada en los servicios que se ejecutan en más de un servidor.

Para admitir la funcionalidad de la cuenta de servicio administrada de grupo, el entorno debe cumplir los requisitos siguientes:
- Debe crear una clave raíz KDS en un controlador de dominio en el dominio.
- Para crear la clave raíz KDS, ejecute el siguiente comando desde el módulo Azure Active Directory para Windows PowerShell en un controlador de dominio de Windows Server.
```powershell
	Add-KdsRootKey –EffectiveImmediately
```
* Puede crear cuentas de servicio administradas de grupo mediante el cmdlet de Windows PowerShell `New-ADServiceAccount` con el parámetro `–PrinicipalsAllowedToRetrieveManagedPassword`.
```powershell
	New-ADServiceAccount -Name LondonSQLFarm 
	-PrincipalsAllowedToRetrieveManagedPassword SEA-SQL1, SEA-SQL2, SEA-SQL3
```

#### Cuentas de servicio administradas delegadas (dMSA)
**==Se incluye en Windows Server 2025==**
Permite a los usuarios pasar de las [cuentas de servicio administradas](Implementaci%C3%B3n%20y%20administraci%C3%B3n%20de%20la%20infraestructura%20de%20identidad.md#cuentas%20de%20servicio%20administradas) a las cuentas de máquina que tienen claves administradas y completamente aleatorias, al tiempo que deshabilitan las contraseñas originales de la cuenta de servicio. La autenticación de dMSA está vinculada a la identidad del dispositivo, lo que significa que solo las identidades de máquina especificadas asignadas en AD pueden acceder a la cuenta. dMSA y gMSA son dos tipos de cuentas de servicio administradas que se usan para ejecutar servicios y aplicaciones en Windows Server. Un administrador administra una dMSA y se usa para ejecutar un servicio o una aplicación en un servidor específico. AD administra una gMSA y se usa para ejecutar un servicio o una aplicación en varios servidores. Otras diferencias son:
- Uso de conceptos de gMSA para limitar el ámbito de uso mediante Credential Guard para enlazar la autenticación de la máquina.
- Credential Guard se puede usar para mejorar la seguridad en dMSA rotando automáticamente las contraseñas y enlazando todos los vales de cuenta de servicio. Las cuentas heredadas se deshabilitan para mejorar aún más la seguridad.
- Aunque las gMSA están protegidas con contraseñas de generación automática y autorrotación de máquinas, las contraseñas siguen sin estar enlazadas a la máquina y pueden ser robadas.
#### Diferencia entre LAPS, MSA, gMSA y dMSA
1. **LAPS (Local Administrator Password Solution)**:
   - Gestiona las cuentas **locales** de administrador en los equipos individuales.
   - Genera contraseñas aleatorias y únicas para cada equipo.
   - Almacena las contraseñas de forma segura en Active Directory, pero sigue siendo para cuentas locales de los equipos.
2. **MSA, gMSA y dMSA (Managed Service Accounts, Group Managed Service Accounts y Delegated Managed Service Accounts)**:
   - Estas son cuentas de **dominio**, diseñadas específicamente para servicios o aplicaciones que requieren autenticación en un entorno de red.
   - Sus contraseñas también son completamente aleatorias, generadas y gestionadas automáticamente por Active Directory.
   - Son ideales para tareas más complejas, como ejecutar servicios en múltiples servidores (gMSA y dMSA) o en servidores individuales (MSA).
### Grupos:
#### Tipos:
* **Seguridad**: se usan para asignar permisos a varios recursos. Puede utilizar grupos de seguridad en las entradas de permisos de las listas de control de acceso (ACL) para ayudar a controlar la seguridad del acceso a los recursos.
* **Distribución**: Las aplicaciones de correo electrónico suelen usar grupos de distribución.
#### Ámbito:
* **Local**: Utilice este tipo de grupo para estaciones de trabajo o servidores independientes, en servidores miembros del dominio que no sean controladores de dominio o en estaciones de trabajo que sean miembros del dominio.
* **Local de dominio**: Este tipo de grupo se usa principalmente para administrar el acceso a los recursos o para asignar derechos y responsabilidades de administración. Los grupos locales de dominio **existen en los controladores de dominio**.
* **Global**:  Este tipo de grupo se usa principalmente para consolidar **usuarios que tienen características similares** (Los miembros solo pueden ser del dominio local y pueden incluir usuarios, equipos y grupos globales del dominio local).
* **Universal**: Este tipo de grupo se usa con más frecuencia en redes multidominio porque combina las características de los grupos locales de dominio y los grupos globales. **Los miembros pueden ser de cualquier parte del bosque de AD DS**.
### Equipos:
 
# [Administración de controladores de dominio de AD DS y roles de FSMO](https://learn.microsoft.com/es-es/training/modules/manage-active-directory-domain-services-flexible-single-master-operation-roles/)

# [Implementación de objetos de directiva de grupo](https://learn.microsoft.com/es-es/training/modules/implement-group-policy-objects/)

# [Administración de características avanzadas de AD DS](https://learn.microsoft.com/es-es/training/modules/manage-advanced-features-of-ad-ds/)

# [Implementación de la nube híbrida con Windows Server](https://learn.microsoft.com/es-es/training/modules/implement-hybrid-identity-windows-server/)

# [Implementación y administración de controladores de dominio de Active Directory de IaaS de Azure en Azure](https://learn.microsoft.com/es-es/training/modules/deploy-manage-azure-iaas-active-directory-domain-controllers-azure/)
