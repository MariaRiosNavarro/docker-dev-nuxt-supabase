# docker-nuxt-dev-supabase

# Docker

(The initial Project/Template is a copy of the LOCAL files of the Tailwind-branch of [this Repository](https://github.com/MariaRiosNavarro/docker-nuxt-dev-small/tree/tailwind), with all the node-modules & .nuxt folder. After copying the repository I re-initialised it as a container with the image I give in that repository). Like that:

```
 docker run -d -p 3010:3000 -v /Users/maria/Documents/GitHub/_DEV/docker/nuxt_supabase:/docker-nuxt --name nuxt-supabase-dev  e7c7d3........

```

where

```
   `docker run -d -p new_port_you_want:port_in_dockerfile -v ABSOLUTE_PATH_YOUR_WORK_APP:PATH_OF_YOUR_IMAGE --name NAME_TO_YOUR_CONTAINER_you_WANT name_or_ID_of_the_image`

```

Also wenn I open http://localhost:3010/, I habe a dev-container.

# Supabase

Install supabase:

`npm install @supabase/supabase-js`

create utils/supabase.ts

```
import { createClient } from "@supabase/supabase-js";

export const supabase = createClient(
  import.meta.env.VITE_SUPABASE_URL,
  import.meta.env.VITE_SUPABASE_KEY
);

```

And  use it



