# think-swoole-crontab
A crontab component base on think-swoole.

## 声明
核心逻辑来自于 [Hyperf](https://hyperf.io) 的 [hyperf/crontab](https://github.com/hyperf/crontab) 组件。非常感谢 Hyperf 为大家提供这么优的组件。

本组件试图让其运行在 ThinkPHP 里（需结合 [think-swoole](https://github.com/top-think/think-swoole) 组件）。

目前还处于初步可用阶段，后续会慢慢完善。

## Requirement
- PHP >= 7.1
- [Composer](https://getcomposer.org/)

## Installation
`composer require overnaive/think-swoole-crontab`

## Documents
- [swoole](https://wiki.swoole.com/#/)
- [hyperf/crontab](https://hyperf.wiki/2.0/#/zh-cn/crontab?id=%e5%ae%9a%e6%97%b6%e4%bb%bb%e5%8a%a1)

## Usage

1. 在 `event.php` 里为 `swoole.init` 事件添加监听类。
```
return [
...
    'listem' => [
        ...
        'swoole.init' => [
            ...
            \ThinkSwooleCrontab\Process\CrontabDispatcherProcess::class,
            ...
        ],
        ...
    ],
...
];
```

2. 在配置文件 `crontab.php` 里添加 `\ThinkSwooleCrontab\Crontab` 实例。
```
return [
    'crontab' => [
        (new \ThinkSwooleCrontab\Crontab())->setName('test-1')
            ->setRule('* * * * * *')
            ->setCallback([Test::class, 'run'])
            ->setMemo('just a test crontab'),
        (new \ThinkSwooleCrontab\Crontab())->setName('test-2')
            ->setRule('* * * * * *')
            ->setCallback([Test::class, 'run'])
            ->setMemo('just another test crontab'),
    ],
];
```

## License
MIT