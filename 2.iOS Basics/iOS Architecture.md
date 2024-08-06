
###### iOS software Architecture
![[../images/Screenshot 2024-07-30 at 5.17.09 PM.png|Screenshot 2024-07-30 at 5.17.09 PM.png]]
###### More detailed view of iOS architecture

![[../images/Screenshot 2024-07-30 at 5.23.36 PM.png|Screenshot 2024-07-30 at 5.23.36 PM.png]]


#### Binary structure of iOS executable

- This is in `Mach-O` format which is three regions: 
   - `Header`: Contains meta data about the application, such as the architecture it supports. 

   - `Load Commands`: Describe the structure and layout of the application, sort of like a table of content that describe the rest of the file.

   - `Data region` : This is divided into segments which is further divided into sections. Among these segments there is `TEXT` segment as first: which is an executable code and a read only executable, it cannot alter itself. There is `DATA` segment is read/write and it contains things like uninitialised variables that will be resolved at runtime.