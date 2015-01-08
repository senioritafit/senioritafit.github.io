---
layout: post
title: Easily drop tables & schemas from Postgres
date: 2014-01-20
updated: 2014-04-08
categories: code postgresql linux
---

I have to refine this into a standalone bash script and move it to GitHub. It provides an easy way to drop multiple tables (or all the tables) in a schema from a terminal.

## Example Usage

```bash
udrop <dbName> <schemaName> [<tableName>]
```

## Full Script

```bash
echodrop() {
    schemaname="${1}"
    tablename="${2}"

    [ ${schemaname} ] && {
        sql="select 'drop table if exists "

        if [ ${tablename} ]; then
            sql=${sql}"'|| schemaname ||'.'|| tablename ||' cascade;' from pg_tables where "
            sql=${sql}"tablename like '%"${tablename}"%' and "
        else
            sql=${sql}${schemaname}".'|| tablename || ' cascade;' from pg_tables where "
        fi

        sql=${sql}"schemaname = '"${schemaname}"';"
        echo ${sql}
    }
}

drop() {
    pg=${1}
    dbname=${2}
    schemaname=${3}
    tablename=${4}

    [ "${pg}" ] || { echo "provide pg information"; return; }
    [ ${dbname} ] || { echo "provide dbname"; return; }
    [ ${schemaname} ] || { echo "provide schemaname"; return; }

    tablesToDrop=$(
        echo $(echodrop ${schemaname} ${tablename}) \
        | ${pg}
    )

    echo "======================================="
    echo ${tablesToDrop} | sed 's/;/;\n/g' | xargs -I '{}' echo "{}"
    echo "======================================="
    read -p "Are you sure you wish to run the above commands? " -n 1
    if [[ ! $REPLY =~ ^[Yy]$ ]]
    then
        echo ""
        return
    fi
    echo ""
    echo "dropping..."
    echo ${tablesToDrop} \
        | sed 's/;/;\n/g' \
        | parallel --gnu -P 4 -I '{}' echo "{}" \
        | parallel --gnu -P 4 echo \
        | ${pg}
}

buildPsql() {
    host=${1}
    username=${2}
    dbname=${3}

    ret='psql -t'
    ret="${ret}"

    [ ${host} ] && { ret="${ret}"' --host '${host}; }
    [ ${username} ] && { ret="${ret}"' --username '${username}; }
    [ ${dbname} ] && { ret="${ret}"' --dbname '${dbname}; }

    echo "${ret}"
}

udrop() {
    dbname=${1}; schemaname=${2}; tablename=${3};
    pg=$(buildPsql "db.urban4m.com" "urban4m" "${dbname}")
    drop "${pg}" "${dbname}" "${schemaname}" "${tablename}"
}
```
