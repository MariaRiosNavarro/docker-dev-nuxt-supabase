# docker-nuxt-dev-supabase

# Docker

The initial project/template is a copy of the local files from the Tailwind branch of this [repository](https://github.com/MariaRiosNavarro/docker-nuxt-dev-small/tree/tailwind), which includes all the node_modules and .nuxt folder. After copying the folder, I initialized it as a container using the image provided in the same repository with the following command:

```
 docker run -d -p 3010:3000 -v /Users/maria/Documents/GitHub/_DEV/docker/nuxt_supabase:/docker-nuxt --name nuxt-supabase-dev  e7c7d3........

```

Here's a breakdown of the command:

```
   `docker run -d -p new_port_you_want:port_in_dockerfile -v ABSOLUTE_PATH_YOUR_WORK_APP:PATH_OF_YOUR_IMAGE --name NAME_TO_YOUR_CONTAINER_you_WANT name_or_ID_of_the_image`

```

After executing this command, I have a dev-nuxt-tailwind-container running when you open http://localhost:3010/.

# Supabase

To start using Supabase:

1. - Go to the Supabase Dashboard and create a new project if you don't have one already.

![readmeImage](/readme_assets/r1.png)

2. - Once your project is created, you can start adding data. You have various options; I'll use tables for this example.

![readmeImage](/readme_assets/r3.png)
![readmeImage](/readme_assets/r4.png)

3. - Define the columns you need for your data. Don't worry about adding more columns later; you can easily update them. Add the data you want in each row. In my example, I create sections for each row to use in my frontend.

![readmeImage](/readme_assets/r5.png)
![readmeImage](/readme_assets/r6.png)

4. - It's crucial to set up table policies; otherwise, when you request data, you'll receive an empty array. Setting up policies is straightforward since Supabase provides several templates to choose from.

![readmeImage](/readme_assets/r7.png)
![readmeImage](/readme_assets/r8.png)
![readmeImage](/readme_assets/r9.png)
![readmeImage](/readme_assets/r10.png)
![readmeImage](/readme_assets/r11.png)
![readmeImage](/readme_assets/r12.png)
![readmeImage](/readme_assets/r13.png)

5. - After setting up your project and adding data, you'll find all the necessary information to connect your project to Supabase. The key information you'll need is the project's address and your key. Make sure to keep these as you'll need them later.

![readmeImage](/readme_assets/ra.png)

# in Your Project

## Installing Supabase

First, install the Supabase JavaScript client in your project:

`npm install @supabase/supabase-js`

## Environment Configuration

Create a .env.local file and add the Supabase URL and key you saved earlier. Always use the prefix VITE if you are using VITE, as I put here in the example.:

```
VITE_SUPABASE_URL=yourURL
VITE_SUPABASE_KEY=yourKey

```

## Create Supabase Configuration

Create a file utils/supabase.ts (or supabase.js) with the following content:

```
import { createClient } from "@supabase/supabase-js";

export const supabase = createClient(
  import.meta.env.VITE_SUPABASE_URL,
  import.meta.env.VITE_SUPABASE_KEY
);

```

## Fetching Data Example

Now, you can fetch your data in your components, like in the following example:

```vue
<script setup>
import { ref, onMounted, provide } from "vue";
import { supabase } from "../utils/supabase.js";

const homeSection = ref([]);

const getHomeData = async () => {
  try {
    // "home_section1" is the name of the Table you want to fetch
    const { data, error } = await supabase.from("home_section1").select();
    if (error) {
      throw error;
    }
    homeSection.value = data;
    console.log(data);
  } catch (error) {
    console.error("Error fetching todos:", error.message);
    console.log(error);
  }
};

onMounted(() => {
  getHomeData();
});

provide("supabaseClient", supabase);
</script>
```

![readmeImage](/readme_assets/result.png)
