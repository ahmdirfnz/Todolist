# my-todo-app

## Project Setup

This project is set up using Vue.js and integrates with Supabase for backend functionality. Follow these instructions to set up the project.

### Step 1: Create a Vue Project
To create a new Vue.js project, run:

### Step 2: Navigate to the Project Directory
Change into your project directory:

### Step 3: Install Supabase
Install the Supabase JavaScript client:

### Step 4: Create .env File
Create a `.env` file at the root folder and add your Supabase URL and ANON Key:

### Step 5: Initialize Supabase
Create a file to initialize Supabase. You can add the following code in a file, for example `src/supabase.js`:
```javascript
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = process.env.VUE_APP_SUPABASE_URL;
const supabaseAnonKey = process.env.VUE_APP_SUPABASE_ANON_KEY;

const supabase = createClient(supabaseUrl, supabaseAnonKey);

export default supabase;

### Step 6: Run Localhost
npm run serve