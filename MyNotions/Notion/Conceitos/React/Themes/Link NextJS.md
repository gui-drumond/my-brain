---
tags:
  - Next
  - React
---
---

  

O link do next é um pouco problemático sua utilização tem várias maneiras:

Começando com sua importação, com um exemplo utilizando o Link para componentização de um menu com chakraUI. O link está ressaltado de amarelo, e com os atributos '==passhref==' pois o Link deve ser passado com um tag html ancor para possa mostrar o preview navegacional (link de direcionamento), sendo assim o passhref força o aparecimento do preview corretamente.

```JavaScript
import Link from 'next/link';

interface NavLinkProps extends ChakraLinkProps{
  children: ReactNode;
  icon: ElementType;
  href: string;
}

export function NavLink({ icon, children, href, ...rest }: NavLinkProps){
  return (
    <Link href={href} passHref>
       <ChakraLink display="flex" { ...rest } align="center">
        <Icon as={icon} fontSize="20" />
        <Text ml="4" fontWeight="medium">
          {children}
        </Text>
      </ChakraLink>     
    </Link>
  );
}
```