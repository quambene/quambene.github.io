<!-- markdownlint-disable MD001 -->

# Fortran

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Subroutines](#subroutines)
- [Modules](#modules)

### Print

``` fortran
program helloWorld
implicit none

character(len = 5) :: my_var
my_var = "world"
print *, 'Hello ', my_var

end program helloWorld
```

### Variables

``` fortran
! constants
real, parameter :: pi = 3.14

! variables
integer :: x ! Declare
x = 4 ! Assign

! pointer
integer, pointer :: p1
allocate(p1)
p1 = 4
Print *, p1
deallocate(p1)
```

### Data types

``` fortran
! Basic types
integer :: i, j, k
integer(kind = 2) :: my_short_var
integer(kind = 4) :: my_long_var
integer(kind = 8) :: my_huge_var
real :: x, y
complex :: z
character (len = 50) :: name
logical :: my_bool

! array
real, dimension(5) :: my_array

! two-dimensional array
real, dimension(5, 5) :: my_matrix

! dynamic array
real, dimension (:,:), allocatable :: my_darray

allocate ( my_darray(my_rows, my_cols) )
deallocate (my_darray)

! derived data type
type User
    character(len = 100) :: username
    character(len = 100) :: email
end type
```

### Control flow

``` fortran
! if-else
if (a < b) then
    ! ...
else if (a == b) then
    ! ...
else
    ! ...
end if

! select case
select case (my_char)
    case('a')
        ! ...
    case('b')
        ! ...
    case default
        ! ...
end select

! do loop
do n = 1, 10, 1
    if (i == 8) then
        cycle
    end if

    if (i == 9) then
        exit
    end if

    if (i == 10) then
        stop
    end if

    ! ...
end do

! while loop
do while (n <= 10)
    ! ...
end do

! nested loop
iloop do i = 1, 3
    ! ...
    jloop: do j = 1, 3
        ! ...
        kloop: do k = 1, 3
            ! ...
        end do kloop
    end do jloop
end do iloop
```

### Functions

``` fortran
function my_func(arg1, arg2)
implicit none
    real :: arg1, arg2
    ! ...
end function my_func
```

### Subroutines

``` fortran
subroutine swap(x, y)
implicit none
    real :: x, y, temp

    temp = x
    x = y
    y = temp
end subroutine swap
```

### Modules

``` fortran
module my_mod
    ! ...
end module my_mod

use my_mod
```
