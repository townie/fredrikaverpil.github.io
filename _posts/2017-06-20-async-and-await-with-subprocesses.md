---
layout: post
title: Async and await with subprocesses
tags: [python]
---

A boilerplate which can be used on Windows and Linux/macOS in order to asynchronously run subprocesses. This requres Python 3.6.

<!--more-->

```python
"""Async and await example using subprocesses

Note:
    Requires Python 3.6.
"""

import os
import time
import platform
import asyncio


async def run_command(*args):
    """Run command in subprocess
    
    Example from:
        http://asyncio.readthedocs.io/en/latest/subprocess.html
    """
    # Create subprocess
    process = await asyncio.create_subprocess_exec(
        *args,
        # stdout must a pipe to be accessible as process.stdout
        stdout=asyncio.subprocess.PIPE)

    # Status
    print('Started:', args, '(pid = ' + str(process.pid) + ')')

    # Wait for the subprocess to finish
    stdout, stderr = await process.communicate()

    # Progress
    if process.returncode == 0:
        print('Done:', args, '(pid = ' + str(process.pid) + ')')
    else:
        print('Failed:', args, '(pid = ' + str(process.pid) + ')')

    # Result
    result = stdout.decode().strip()

    # Return stdout
    return result


async def run_command_shell(command):
    """Run command in subprocess (shell)
    
    Note:
        This can be used if you wish to execute e.g. "copy"
        on Windows, which can only be executed in the shell.
    """
    # Create subprocess
    process = await asyncio.create_subprocess_shell(
        command,
        stdout=asyncio.subprocess.PIPE)

    # Status
    print('Started:', args, '(pid = ' + str(process.pid) + ')')

    # Wait for the subprocess to finish
    stdout, stderr = await process.communicate()

    # Progress
    if process.returncode == 0:
        print('Done:', args, '(pid = ' + str(process.pid) + ')')
    else:
        print('Failed:', args, '(pid = ' + str(process.pid) + ')')

    # Result
    result = stdout.decode().strip()

    # Return stdout
    return result


def run_asyncio_commands(tasks):
    """Run tasks asynchronously using asyncio and return results

    Note:
        By default, Windows uses SelectorEventLoop, which does not support
        subprocesses. Therefore ProactorEventLoop is used on Windows.
        https://docs.python.org/3/library/asyncio-eventloops.html#windows
    """

    if platform.system() == 'Windows':
        loop = asyncio.ProactorEventLoop()
        asyncio.set_event_loop(loop)
    else:
        loop = asyncio.get_event_loop()

    commands = asyncio.gather(*tasks)  # Unpack list using *
    results = loop.run_until_complete(commands)
    loop.close()
    return results


if __name__ == '__main__':

    start = time.time()

    if platform.system() == 'Windows':
        # Commands to be executed on Windows
        commands = [
            ['hostname']
        ]
    else:
        # Commands to be executed on Unix
        commands = [
            ['du', '-sh', '/var/tmp'],
            ['hostname'],
        ]

    tasks = []
    for command in commands:
        tasks.append(run_command(*command))
    

    # # Shell execution example
    # tasks = [run_command_shell('copy c:/somefile d:/new_file')]

    # # List comprehension example
    # tasks = [
    #     run_command(*command, get_project_path(project))
    #     for project in accessible_projects(all_projects)
    # ]

    results = run_asyncio_commands(tasks)
    print('Results:', results)

    end = time.time()
    print('Script ran in', str(end - start), 'seconds')

```
