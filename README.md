/**
 * Генерация набора коммитов.
 *
 * @param  string[]   $map          Карта коммитов в виде массива из 7 строк по 52 символа каждая
 * @param  \DateTime  $firstSunday  Дата последнего воскресенья год назад
 * @return array
 */
function generateCommits($map, $firstSunday)
{
    $commits = [];
    $count = 7 * 52;
    $date = clone $firstSunday;

    // Идём по всем символам карты коммитов, вычисляя неделю и день недели
    for ($day = 0, $weekDay = 0; $day < $count; $day++) {
        $week = intval($day / 7);
        $char = substr($map[$weekDay], $week, 1);
        if ($char !== ' ') {
            $commits[$date->format('Y-m-d')] = $char === '#' ? 20 : 10;
        }
        // Переходим к следующему дню
        $date->add(new DateInterval('P1D'));
        $weekDay = ($weekDay + 1) % 7;
    }

    return $commits;
}
