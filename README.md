# cowsquare-schema-setup
How to set up a schema on cowsquare

1. Design schema. [This site](https://ondras.zarovi.cz/sql/demo/) helps you visualize and generate a schema in PostgreSQL.

2. Create new schema in Hasura using SQL.

```sql
create schema demo_ypo
    create table demo_ypo.hidden_file_table (
        id uuid DEFAULT gen_random_uuid() NOT NULL,
        "name" text NOT NULL,
        link text NOT NULL,
        "key" text NOT NULL,
        PRIMARY KEY(id)
    )
    create table demo_ypo.hidden_index_column (
        id uuid DEFAULT gen_random_uuid() NOT NULL,
        table_name text NOT NULL,
        column_name text NOT NULL,
        tc_name text NOT NULL,
        priority integer NOT NULL,
        PRIMARY KEY(id)
    )
    create table demo_ypo.hidden_index_table (
        id uuid DEFAULT gen_random_uuid() NOT NULL,
        table_name text NOT NULL,
        tc_name text NOT NULL,
        priority integer NOT NULL,
        relation_tables jsonb,
        "group" text,
        PRIMARY KEY(id)
    )
    create table demo_ypo.hidden_pdf_templates (
        id uuid DEFAULT gen_random_uuid() NOT NULL,
        "name" text NOT NULL,
        table_name text NOT NULL,
        "content" text NOT NULL,
        PRIMARY KEY(id)
    )
    create table demo_ypo.hidden_wizards (
        id uuid DEFAULT gen_random_uuid() NOT NULL,
        "name" text NOT NULL,
        flow jsonb NOT NULL,
        PRIMARY KEY(id)
    )
    create table demo_ypo.hidden_email_center (
        id uuid DEFAULT gen_random_uuid() NOT NULL,
        "from" text NOT NULL,
        "to" text NOT NULL,
        subject text NOT NULL,
        "content" text,
        user_id uuid NOT NULL,
        created_at timestamp with time zone DEFAULT now() NOT NULL,
        attachments jsonb,
        status text DEFAULT 'processing'::text,
        PRIMARY KEY(id)
    )
    create table demo_ypo.hidden_page_table (
        "id" uuid PRIMARY KEY DEFAULT uuid_generate_v4(),
        "name" text,
        "path" text,
        "rows" jsonb
    )
```

3. Remember to change "id" to `id uuid DEFAULT gen_random_uuid() NOT NULL`

4. Navigate to the `Public` DB
   1. Insert Row in `organizations`
   1. Insert Row in `users_organizations` with `organization_id` and your `user_id`, with `role` as `admin`.

5. Update `hidden_index_table` for display purposes.

6. Remove all Foreign Keys in all tables

7. Create Object Relationships.

8. Hasura > Table > Permissions, update Permissions for Owner. 
